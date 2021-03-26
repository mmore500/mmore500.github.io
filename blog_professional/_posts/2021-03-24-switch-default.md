---
layout: post
title: "Unreachable Switch Statement Default Cases"
date: 2021-03-24
no_toc: true
---

Standard C and C++ requires `switch` statements to behave harmlessly if on a value that not covered by one of their `case`'s.
For example, in this case
```cpp
switch( i ) {
  case 0:
    j+=k;
    break;
  case 1;
    j*=k;
    break;
  case 2:
    j/=k;
    break;
}
```
If `i` wasn't 0, 1, or 2, the `switch` statement would just roll on by without anything happening to `j`.

Behaving harmlessly is good, except that it's not free.
In practice, this means that every time the `switch` statement executes it has to bounds-check `i`.
In really tight loops, for example in a [byte-code interpreter](https://eli.thegreenplace.net/2012/07/12/computed-goto-for-efficient-dispatch-tables) where each case statement represents an instruction on a virtual CPU, this bounds-checking can add up!

Enter [`__builtin_unreachable()`](https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html), a compiler intrinsic that lets you double-dog swear   that a section of code will never execute.
It's not standard, but GCC and Clang at least both know about it.
Getting the compiler to take your word that certain execution paths will never execute is useful for all sorts of mischief, but I wondered whether it might prove useful in this particular problem of disabling `switch` bounds-checking.

Basically this would look like something along the lines of,
```cpp
switch( i ) {
  case 0:
    j+=k;
    break;
  case 1;
    j*=k;
    break;
  case 2:
    j/=k;
    break;
  default:
    __builtin_unreachable();
}
```


To the compiler-explorer-&-quick-bench-mobile!!
:bat:

Here's an assembly snippet from a small example I threw together [on Godbolt](https://godbolt.org/z/TrqKv77G6).
```
unreachable_default(int):
        mov     edi, edi
        mov     eax, DWORD PTR CSWTCH.2[0+rdi*4]
        ret
no_default(int):
        xor     eax, eax
        cmp     edi, 3
        ja      .L3
        mov     edi, edi
        mov     eax, DWORD PTR CSWTCH.4[0+rdi*4]
```

With the `unreachable_default` function, we can skip a `cmp` (compare) and `ja` (jump if) instruction.
I assume that in the `no_default` function those instructions were being used for the aforementioned bounds-checking.

But, does it go brrr?
[Looking at this graph](https://www.youtube.com/watch?v=sIlNIVXpIns), it does indeed seem to go brrr.

![benchmarking result](/resources/switch-default-microbench.jpg){:width="100%"}

Compiling with Clang, adding an unreachable default case gives ~1.3x speedup [on a toy example](https://quick-bench.com/q/1cObPCIkz3g44gHWFWeTkKDgp1Q).
Even though I was able to see some changes in the compiler output (so `_unreachable_default()` was doing *something*) [I wasn't able to see any speedup on GCC, though](https://quick-bench.com/q/ycTTednxWKAsGKd3JsRG9YH9bx8).

Kind of a nifty trick!
I've gone ahead and pasted it in to some of my projects, like [signagp-lite](https://github.com/mmore500/signalgp-lite), that do byte-code interpretation in a tight loop.
I did add a (debug-mode only) assert in right before the `__builtin_unreachable()`... you know, in order to properly check myself when I inevitably wreck myself.
:man_shrugging:

## Let's Chat

Comments?
Questions?
I'd love to hear about any related hacks you're up to!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">it&#39;s been forever, but new blog post!!! <br><br>this one on mischief with __builtin_unreachable() default switch cases<br><br>perfect for the extra percent of unsafe bytecode interpreter fun 🍹🏖️💣<a href="https://t.co/rBJCM8nnJt">https://t.co/rBJCM8nnJt</a></p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1374891036934295555?ref_src=twsrc%5Etfw">March 25, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
