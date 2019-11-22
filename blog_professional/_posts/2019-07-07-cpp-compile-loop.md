---
layout: post
title:  "C++ Compile-Time For Loop"
date:   2019-07-07
no_toc: true
---

## A More-Prettier Compile-Time For Loop?

Today, I've been working on a function that templates on a `size_t` value.
To test it extensively, I needed to iterate over a range of template values at run time.

The answer, of course, is recursive SFINAE business.
Here's the original approach I used, adapted from [Simon Praetorius' blog post](spraetor.github.io/2015/12/26/compile-time-loops.html).

```c++
template <size_t I, size_t N>
struct ForEach {

  static void item() {

    // do whatever
    std::cout << I << std::endl;

    // recurse upwards
    ForEach<I+1,N>::item();

  }

};

// base case
template <size_t N>
struct ForEach<N,N> { static void run() {} };

int main () {
  ForEach<10, 0>::item();
  return 0;
}
```


I made [good use of `if constexpr`](https://blog.tartanllama.xyz/if-constexpr/) to write something sligly different.
Maybe a little prettier.

```c++
#include <iostream>

template <size_t N>
struct ForEach {

  template <size_t I>
  static void item() {

    // do whatever
    std::cout << I << std::endl;

    // recurse upwards
    if constexpr (I+1 < N) ForEach<N>::item<I+1>();

  }

};

int main () {
  ForEach<10>::item<0>();
  return 0;
}
```

## Extra-Special Spicy Footnote

If you want to use a templated class' templated function inside the compile-time for loop, you have to use some [special syntax or the compiler gets confused and sad](https://stackoverflow.com/questions/610245/where-and-why-do-i-have-to-put-the-template-and-typename-keywords).

This example demonstrates with the [Empirical C++ library](https://github.com/devosoft/Empirical).

```c++
#include <iostream>

#include "tools/BitString.h"

template <size_t N>
struct ForEach {

  template <size_t I>
  static void item() {

    // do whatever
    emp::BitString<N> bs; // templated class
    bs.template ROTR_SELF<I>(); // spicy syntax for
                                // templated class' templated function

    // recurse upwards
    if constexpr (I+1 < N) ForEach<N>::item<I+1>();

  }

};

int main () {
  ForEach<10>::item<0>();
  return 0;
}
```

If you want to use nested compile-time for loops, you need to use the static version of the special spicy syntax.

```c++
#include <iostream>

template <size_t N>
struct ForEachInner {

  template <size_t I>
  static void item() {

    // do whatever
    std::cout << " " << I << std::endl;

    // recurse upwards
    if constexpr (I+1 < N) ForEachInner<N>::item<I+1>();

  }

};

template <size_t N>
struct ForEachOuter {

  template <size_t I>
  static void item() {

    // do whatever
    std::cout << I << std::endl;
    ForEachInner<I>::template item<0>(); // inner compile-time for loop
                                         // spice level: extreme

    // recurse upwards
    if constexpr (I+1 < N) ForEachOuter<N>::item<I+1>();

  }

};

int main () {
  ForEachOuter<10>::item<1>();
  return 0;
}
```

Hooray for uggo obscure C++ syntax.

## Let's Chat

Comments? Questions?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">wrote a micro-post on C++ compile-time &quot;for loops&quot;<br><br>feat. a dash of spicy extra-obscure uggo C++ syntax 🤷‍♂️<a href="https://t.co/oN7d8sQTCv">https://t.co/oN7d8sQTCv</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1147926107951443968?ref_src=twsrc%5Etfw">July 7, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
