---
layout: post
title:  "An 11th Way to Convert a char to a string in C++"
date:   2020-02-25
no_toc: true
---

If by some miracle of search engine optimization you landed here first just googling around for a C++ code snippet or for some reason you found [Techie Delight](https://www.techiedelight.com/)'s listicle [10 ways to convert a char to a string in C++](https://www.techiedelight.com/convert-char-to-string-cpp/) inadequately delightful, here's your payoff right out of the gate.

```cpp
std::string res{'c'};
```

Great!
You're free to go...

![](/resources/char-to-string-smartz.jpg){:width="100%"}

## or: How I Learned that Braces and Parens Aren't the Same Thing

... but, if you feel like sticking around for a brief debugging fable (perhaps even conveying something of a moral) you're also welcome to stick around!
:upside_down_face:

The story starts with [@rodsan0](https://github.com/rodsan0) & I doing [some pair programming](https://github.com/devosoft/Empirical/pull/242) on a command line argument parsing tool in [our lab's software library](https://github.com/devosoft/Empirical/).
One of the POSIX-y features we were working on was support for stringing together single-letter options (a la `ls -lvd`).

![](/resources/char-to-string-standardize.jpg){:width="100%"}

We found ourselves needing to grab the single-letter chars out of argument strings and then convert them back to strings to do lookups in a command de-aliasing map.
"This should be an easy no-brainer thing to do," we cheerfully assumed.

We poked through the [first](https://www.techiedelight.com/convert-char-to-string-cpp/) [half](https://stackoverflow.com/questions/17201590/c-convert-from-1-char-to-string) of the first page of the Google results for "char to string C++."
The string [fill constructor](http://www.cplusplus.com/reference/string/string/string/), which takes a repeat-count and a character as arguments, seemed a good fit.
Bippity-boppity-boo... here's what we typed up:

```cpp
std::string res{1, 'c'};
```

The lookups weren't working how we expected, so we tried printing out the lookup keys we were generating.
They looked how we would expect, with

```cpp
std::cout << res << std::endl;
```

yielding

```
c
```

Imagine our surprise 30 minutes later when we discovered that,
```cpp
res != "c"
```

Digging in further, we discovered
```cpp
res.size() == 2
```

Then, we found that the first character of the generated string was "[ASCII Start of Header](https://theasciicode.com.ar/ascii-control-characters/start-of-header-ascii-code-1.html)," followed by the expected character `c`.
Wut.

As these things do when you figure them out, the answer hit us with all of the subtlety [of a Hefty bag filled with vegetable soup](https://dysonology.wordpress.com/2011/05/06/56-bestworst-similes-used-in-high-school-exams/).

![](/resources/char-to-string-vector.jpg){:width="100%"}

We quickly confirmed that
```cpp
std::string res{97, 'c'} == "ac"
```

We weren't using the fill constructor at all!
We were using the *initializer list* constructor.

To get the fill constructor we expected, we should have been using *parens*
```cpp
std::string res(1, 'c');
```

Simple enough, but how did we end up in this particular time-wasting pickle?
Well, being a [Good C++ Dilettante](https://www.quora.com/Why-do-some-famous-programmers-e-g-Richard-Stallman-Linus-Torvalds-Ken-Thompson-and-Brian-Kernighan-dislike-C++-What-are-the-alternatives/answer/Jason-Martin-168), somewhere along the way I had picked up the notion to just always throw braces on when creating new objects and feel like a good modern C++ [good boy](https://animalchannel.co/photos-dogs-before-after-called-good-boys/).

Wow.
Much [core guideline](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) ["ES.23: Prefer the `{}`-initializer syntax"](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#es23-prefer-the--initializer-syntax).
Good job me.

But, as with all things C++, in ES.23 there is also a clearly documented...
> **Exception**
>
>
> For containers, there is a tradition for using `{...}` for a list of elements and `(...)` for sizes:
> ```
> vector<int> v1(10);    // vector of 10 elements with the default value 0
> vector<int> v2{10};    // vector of 1 element with the value 10
>
> vector<int> v3(1, 2);  // vector of 1 element with the value 2
> vector<int> v4{1, 2};  // vector of 2 element with the values 1 and 2
> ```

On the plus side, this rabbit hole introduced us to the little "11th Way" initializer list approach the post opened with!

## Lesson of the Day

Anyways, here's your "so-called promised fable:"
doing things to Follow The Rule will only get you so far if you don't also Understand The Rule.

As [Kate Gregory eloquently points out](https://www.youtube.com/watch?v=tTexD26jIN4), writing good C++ is an exercise in continually learning C++.
In C++ and other (?) parts of life (??), keeping alert for the things we do but don't really understand can be a launching point to gaining understanding!

Braces and parens are not the same thing.

![](/resources/char-to-string-initializations.gif){:width="100%"}

## Let's Chat

I would love to hear your thoughts, questions, and comments RE: char-to-string conversion & lifelong C++ learning!!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">new <a href="https://twitter.com/hashtag/cpp?src=hash&amp;ref_src=twsrc%5Etfw">#cpp</a> blog post:<br>* the teeniest, tiniest, most trivial code snippet converting char to string<br>* 1 quality jif &amp; 3 quality memes<br>* also Reflections on the perpetual process of learning C++???<br> <a href="https://t.co/elEOckMWzh">https://t.co/elEOckMWzh</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1232532660297379840?ref_src=twsrc%5Etfw">February 26, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
