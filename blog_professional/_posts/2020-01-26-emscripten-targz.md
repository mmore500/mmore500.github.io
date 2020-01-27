---
layout: post
title:  "So You Want To Retrieve and Extract .tar.gz Archive with Empscripten"
date:   2020-01-26
no_toc: true
---

As part of ongoing work with [my scientific project's cool cool web interface](https://mmore500.github.io/dishtiny/), I spent this afternoon and evening figuring out how to download configuration and data files into the browser.
I figured I should share what I learned!

Emscripten's nifty [file packaging](https://emscripten.org/docs/porting/files/packaging_files.html), which prepares elements of the browser file system at compile time and packages it with your "executable," had been my go to for a while.
However, it became necessary to be able to swap out file contents without recompiling so this no longer cut the mustard.

The configuration and data files I work with are organized in a hierarchical structure with meaningful filenames that have unpredictable components.
I could try to have the user specify the filenames one by one in the browser and have the user copy them down one by one, but that would be brittle and annoying.

Instead, I'd like to grab them all at once.
A [tar archive](https://en.wikipedia.org/wiki/Tar_(computing)) which allows entire directory structures to be packaged into a single file are an appealing choice.

My files are big and repetitive, so I'd like to use [gzip compression](https://en.wikipedia.org/wiki/Gzip) so they'll load up faster.

Compressing and extracting `.tar.gz` archives at the terminal is easy[-ish](https://xkcd.com/1168/).
Getting it going from a C++ program inside Emscripten's browser sandbox?
A little harder, but once I found the right pieces to slot together not actually too bad.

In this blog, I'll briefly discuss each the components I assembled and tweaked to create a minimal working example of retrieving and extracting a `.tar.gz` archive with Emscripten.
Then, I'll walk you through getting the minimal working example actually running on your own machine.

You can find all the complete minimal working example [on Github](https://github.com/mmore500/emscripten-targz).

## `inflate.h`

The first step is to decompress (or "inflate") the archive.
The `zlib` project, which has [a maintained port for Emscripten](https://github.com/emscripten-ports/zlib), provides a `gzFile_s` file handle analogous to the C-style `FILE` handle to get at a gzipped file.

So, we just do some [K & R](https://stackoverflow.com/questions/10195343/copy-a-file-in-a-sane-safe-and-efficient-way) B.S. to copy content from the gzipped file over to a regular file.

## `untar.h`

Now we just have a regular old `tar` file.
But we still have to do a little more work.
This header provides `untar`, which reads that `tar` archive into the file system.

I borrowed most of the code in this header from Tim Kientzle's [untar](https://raw.githubusercontent.com/libarchive/libarchive/master/contrib/untar.c) and added support for long filenames stored using [@LongLink](https://stackoverflow.com/questions/2078778/what-exactly-is-the-gnu-tar-longlink-trick).

Besides standard library components, `untar.h` has no dependencies.

## `main.cc`

We use [`emscripten_wget`](https://emscripten.org/docs/api_reference/emscripten.h.html#c.emscripten_wget) to copy the `.tar.gz` archive into Emscripten's in-browser file system.
Then, we call `inflate` and `untar` in sequence.
Finally, we clean up the original `.tar.gz` file (don't need it anymore!) and print some results to make sure everything worked.

This file contains the interesting code bits and bops you'd plug into your project if you were trying to do this yourself, so I've included a listing here for your edification. :apple:

```cpp
#include <iostream>
#include <stdio.h>
#include <fstream>
#include <set>

#include <experimental/filesystem>

#include <zlib.h>
#include <emscripten.h>

#include "inflate.h"
#include "untar.h"

const std::string source_filename{"example.tar.gz"};

int main() {

  // this call to copy down the tar.gz archive is blocking
  // you have to compile with -s ASYNCIFY=1 to use it
  // emscripten_async_wget doesn't require ASYNCIFY
  emscripten_wget(
    "http://127.0.0.1:8000/example.tar.gz",
    source_filename.c_str()
  );

  auto file = gzopen(source_filename.c_str(), "rb");
  auto temp = std::tmpfile();

  // unzip into temporary file
  inflate(file, temp);

  gzclose(file);
  std::rewind(temp);

  // untar into present working directory
  untar(temp, "temp");

  // deletes temporary file
  std::fclose(temp);

  // remove the original .tar.gz archive... we don't need it anymore!
  std::experimental::filesystem::remove(source_filename);

  // print results
  std::cout << "time to print results!" << std::endl;

  for (const auto & filename : std::set{
    "example/example_file.txt",
    "example/example_directory/another_file.txt"
  }) {

    std::cout << "filename: " << filename << std::endl;

    std::cout << "  size: " << std::experimental::filesystem::file_size(filename) << std::endl;

    std::cout << "  content: " << std::endl;

    std::ifstream file{filename};

    std::string line;
    while(getline(file, line)) std::cout << "    " << line << std::endl;

  }

  std::cout << "all done" << std::endl;

}
```

## `index.html`

This html file gives us something to look at when we serve up the minimal working example. :squirrel:

## `example.tar.gz`

This is the example `.tar.gz` archive we want to retrieve and extract.

```
example
├── example_directory
│   └── another_file.txt
└── example_file.txt
```

## Compile & Run

You'll need a working copy of Emscripten to start with.
Emscripten's [Getting Started](https://emscripten.org/docs/getting_started/index.html) page has instructions on getting that set up.
I used version 1.38.28.

Grab the minimal working code.

```bash
git clone https://github.com/mmore500/emscripten-targz.git
cd emscripten-targz
```

Compile with `emcc` with flags to request zlib and asyncify.

```bash
emcc -std=c++17 -s USE_ZLIB=1 -s ASYNCIFY=1 -O3 main.cc -o example.js
```

All that's left to do is serve it up...

```bash
python3 -m http.server 8000
```

...and surf over to [http://127.0.0.1:8000](http://127.0.0.1:8000) and pull up the JavaScript console in your developer tools. :sunglasses:

## Let's Chat

I would love to hear your thoughts, questions, and comments RE: Emscripten `.tar.gz` kung fu!!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">throwing together this Quality Blog on retrieving and extracting .tar.gz archives with <a href="https://twitter.com/hashtag/Empscripten?src=hash&amp;ref_src=twsrc%5Etfw">#Empscripten</a> at 230 am ...<br><br>so I&#39;ll let you guess how much fiddling and twiddling it took to get working 🙃 🙃🙃<a href="https://t.co/ovolzUmqot">https://t.co/ovolzUmqot</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1221698974379196418?ref_src=twsrc%5Etfw">January 27, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
