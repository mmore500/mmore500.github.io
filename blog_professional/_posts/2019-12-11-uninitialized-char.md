---
layout: post
title:  "So You Want a vector of Uninitialized Elements?"
date:   2019-12-11
no_toc: true
---

In [ongoing work to parallelize evolution-of-multicellularity research software]({% post_url 2019-11-15-mpi-example %}), we want to interface the cleverly-named serialization framework [cereal](http://uscilab.github.io/cereal/) with the matter-of-factly named [Message Passing Interface](https://en.wikipedia.org/wiki/Message_Passing_Interface).
The basic idea is to take C++ objects, use cereal to turn them into bitstreams (plain Jane 0's and 1's), and then use MPI to send the bitstreams between compute nodes.
However, the cereal interface is built around stream objects and the MPI interface is built around raw, contiguous memory (yay, void pointers 'n sizeofs).

The class `std::stringstream` provides a workable, but potentially inefficient, solution.
First we would truck the data into a `std::string` using the `.str()` method.
Then, we would call `.c_str()` on the string to get a pointer to the beginning of a contiguous allocation containing our data!
The fundamental problem here is that [`std::stringstream` doesn't necessarily store data contiguously](https://stackoverflow.com/a/1877528).
Implementations might, in fact, store data in disjoint chunks, and the interface reflects that fact.

So, to reduce unnecessary copying (for time and space efficiency), we want a stream (which cereal can talk to) that writes to contiguous memory we can then hand off to MPI.
[@nateriz](https://github.com/nateriz) and I got to work and [wrote a `ContiguousStream`](https://github.com/devosoft/Empirical/pull/253) class for the [Empirical C++ library](http://github.com/devosoft/Empirical) that does just that.

## The Problem

Under the hood, our `ContiguousStream` implementation puts streamed-in data into a `std::vector<char>`.
That way, we can increase capacity in [a happy modern C++-y way](http://www.stroustrup.com/bs_faq2.html#realloc).

But, we do a little unnecessary work here: when we create the vector and each time we call `.resize()` on it C++ helpfully zero-initializes the fresh space.
(Translation: it runs through that memory and sets it all to zero).
This zero-initialization work's not actually helpful for us because we only ever care about what's in memory after we've streamed data into it.
(We don't care about memory we've allocated but haven't streamed to yet.)

If a user were to use fresh `ContiguousStream` for each output task (instead of `.Reset()`-ing an existing `ContiguousStream`), the amount of wasted zero-initialization work done would be roughly proportional to the amount of data written.
Yuck!

## An Idea

We want a vector that doesn't waste time zero-initializing members.

What to do, what to do?

We could write an entire vector implementation that *doesn't* default-initialize elements when constructed with a size parameter or extended with `.resize()`.
Andre Offringa actually did do this and wrote it up as [a great blog post with extensive profiling results](http://andreoffringa.org/?q=uvector).
It's an effective solution, but it's also [1.2k lines of neither easy nor simple](http://andreoffringa.org/p/uvector/uvector.h) (and in this case, also copyleft-licensed :man_shrugging:).

What if we just wrapped our data members in a struct that didn't zero-initialize them?
For `char` (our target in this case) this looks along the lines of,

```c++
struct uninitialized_char {

  char val;

  // necessary to prevent zero-initialization of val
  uninitialized_char() { ; }

  // make implicitly convertible to char
  operator char() const { return val; }

};
```

Then, we could just make a vector of those instead (e.g., `std::vector<uninitialized_char>`).

## Will It <strike>Blend</strike> Compile?

Yes, it does.

Peeking at the intermediate representation `std::vector<uninitialized_char>` compiles down to, we can actually see the machine code for zero-initialization go away!

<iframe width="800px" height="1200px" src="https://godbolt.org/e?hideEditorToolbars=true#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAM1QDsCBlZAQwBtMQBGAFlICsupVs1qhkAUgBMAISnTSAZ0ztkBPHUqZa6AMKpWAVwC2tLgAZSW9ABk8tTADljAI0zEQkyaQAOqBYXVaPUMTcx8/ALpbeycjV3dPRWVMVUCGAmZiAmDjU04LJRU1OnTMgmjHFzcPLwUMrJzQ/MV68rtKuOrPAEpFVANiZA4AcikAZjtkQywAanExnVdaZAQjTIBrAHollbXidYA6BHnscTMAQTPzuuIDVRnfJWIAfQNaOwC2PAAvTHRnlaZOYAdlkFyuMxmgOIMwAbmx5mDLhdIahvG5mEQYdCIN0oXQ6iDpDNiJgCANaHCEWNieJgQARK5MhmIpkXG53AgzN4fNRfX7/aFEtnnSFC%2BGsVnglHc97vPmsH5/AEITK4olzGkgxnS0UzNEYrFQ1XEdVoWiEunE0nk4iUiWI7UiumMmki2GoPDoWW89VWiGQmZ1dAgECwlJY%2BY6HnyvD85XQk5wlLPZgQfKSbjdKV6yE7VYbUP01AOVAEADy3jURiVEHDyFT2bd4IZc11Hq9Dz8blecsIftBAchwdD9cjC0ePZjn0VApVmST9eeznTZkzTaRgZm%2Bb26yLJbLlertaXzg3zPpbeR5w73t9eP9MuHBBDYYjJCjibG2GTDeQq/XHMtx3QsQGLUsKyrPAa1%2BOsU2Qc8W0vEVhl6VgQGGABWYZSFMYYzBw1AMJ0OQ5CDfpBkwOZJDGTgcIIDCCO6Xo90wix0OGbgcLwgjSCI4YcIUEALAY/DUNIOBYCQNAjG8PB2DICgIBkuSFJQYRRAATjMCwqHkgg3CEiBnEYnDnDsTIAE8MLo0gZKMLQK1oVhrLE0gsDWUR2FM9y8FJVJwyEtzMAADxSAwDJsnC7AMjjeMVZxiCsvQsCi0gCGIaCot6Gh6CYNgOB4fhBA0sRSJkIQ8GcITYFoZgHJAED9lIcN3GGHgmN6NFigtDCAFpg3mekJBkOROGBGY%2BvLMZBOSVINAgKxGlMGjLG0CpYniEAxgANnCfweuWjwxn2yJaA2qp3F2pIijSVojvGm6IzusoLs6K69rqMoHuBFpXvaTbql23oFAooYuDQjDsNwnz%2BJCgAOHa%2Bp27goVKmZNIOMwsZmCBcEIEhqNo0gZj0WT5LcInODxEjRpkejTOY0hWPYjCuJhtz%2BME4T0sZyHhkkbjYYwhmxKZ1r/A0bggA%3D%3D"></iframe>

The [Compiler Explorer](https://godbolt.org/) snippet above compares three functions:
1. `uninit`: construct a 1024-byte `std::vector<uninitialized_char>`,
2. `poser_uninit`: construct a 1024-byte `std::vector<poser_uninitialized_char>`, and
3. `init`: construct a 1024-byte `std::vector<char>`.

(There's also some fancy footwork to prevent the vectors we're interested from being completely optimized away.)

We can see that Clang generates shorter intermediate assembly for `uninit` than `init`.
Inspecting in greater detail, we can see a call to `memset`, a prime suspect for actually carrying-out zero-initialization, present in `init` but not in `uninit`.
It seems that `uninitialized_char` is working how we expect!

I also included the struct `poser_uninitialized_char` (hooked into `poser_uninit`) to illustrate the role of `uninitialized_char`'s custom constructor.
It appears that in `poser_uninitialized_char` (which uses a default constructor) the `val` member is still being zero-initializedd.

## Is It <strike>on Fleek</strike> Performant?

Yes, it is.

I benchmarked the impact of `uninitialized_char` char on 1024-byte vector creation using the nifty [Quick C++ Benchmark](http://quick-bench.com/) web tool.

![benchmarking results](/resources/uninitialized-char-quick-bench.png){:width="100%"}

You can see a ~1.8x speedup when using `std::vector<uninitialized_char>` compared to vectors of raw `char`'s or the wrapper class lacking the custom constructor that eschews member zero-initialization.

The benchmarking code and results are live [here](http://quick-bench.com/GB8SEE5N2I_Q4qcYUl7UjvTg-OY).

## Let's Chat!

Questions? Comments? Concerns? Other ideas?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">wrote a cute lil&#39; blog post 🐶 on a cute lil&#39; <a href="https://twitter.com/hashtag/cpp?src=hash&amp;ref_src=twsrc%5Etfw">#cpp</a> hack 😽 to make vectors go fast by skipping zero-initialization of contents<br><br>I address key q&#39;s such as<br>1. will it b̶l̶e̶n̶d̶ compile<br>2. is it o̶n̶ ̶f̶l̶e̶e̶k̶ performant<br><br>uwu 🔜 <a href="https://t.co/B9mRtQDdJd">https://t.co/B9mRtQDdJd</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1204961151643197440?ref_src=twsrc%5Etfw">December 12, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
