---
layout: post
title: "Optimizing HDF5 files for better storage and IO"
date: 2020-08-04
---

| ratio | time (s) | .h5 size (MiB) | .tar.gz size (MiB) |
|:-----:|:--------:|:--------------:|:------------------:|
|     0 |   229.19 |            145 |                5.7 |
|     1 |   260.37 |             12 |                6.6 |
|     3 |    293.7 |             12 |                6.4 |
|     6 |   310.78 |             11 |                5.5 |
|     9 |   573.11 |             11 |                5.8 |

## A storage problem

Sometimes, when it comes to scientific research, you want to gather data to later analyse.
In the physical world this is a complicated process.
You must first define what data you want to collect, then determine specific bounds on that collection (such as acceptable uncertainty, error, range, etc), and from there figure out what tool will be used.

Only then will you be able to start measuring.

The digital world, however, is discrete and fully deterministic.
If you have a well-behaved program that is fed the same starting inputs, you are guaranteed to have the same result: its whole state is determined at every point in time.
This effectively means that all the data you could ever possibly need is already there, and you just need a way to pull it out and store it.

In the case of dishtiny, the state of every digital cell (such as its functions, its resources, its age, its connections to other cells) comprises this data.

A naive approach would be to take a snapshot of dishtiny’s memory at every interval of time.
However, this would both slow down execution (due to having to pause the program while the snapshot is taken) and take up a lot of storage (imagine a handful of gigabytes being written to disk every second).

We can definitely do better.

The best approach is to proceed as if it were a physical system: by defining variables to collect.
Thus, we would only store the relevant data with every update, saving a lot of space.
However, this means we must know what data will be relevant for our analysis a priori, which isn’t always possible and greatly limits changing our objectives after an a posteriori analysis.
Oh well, we can’t have everything.

In this particular case, we collect metadata about the run, as well as each of the state of each square of the grid.
A detailed overview can be found [here](link to github gist with list of datasets).

While space-time is (probably) a continuum, dishtiny deals with time in discrete intervals.
These cough, “update intervals,” are bound by the computer in which the program runs.
Upgrade to a faster computer and you will have more updates per second.

Something interesting about the digital world, is that, much like the real one, change happens slowly.
The state of the cells remains relatively unchanged from update to update, and evolution can only be appreciated when analysing a bigger timeframe.
Due to this, we can safely store the change that happens between each update, in turn decreasing the data stored significantly.
However, deltas like these are hard to implement manually.

Why HDF5?

Interestingly, one does not have many choices when it comes to storing data for scientific purposes.
A CSV file would be the first approach to try, but if the plan is to store anything over a couple megabytes of data, this soon becomes a pain to maintain: one has no intuitive way to aggregate by runs, updates, types of data; and it soon becomes a problem to deal with the linearly-growing file size.
Moreover, plaintext files are easily corrupted, have no multithread support, and must be compressed manually.

An H5 file, on the other hand, supports all of the former.
The file layout is a bit hard to get your mind wrapped around at first—it is more akin to a filesystem with folders and files in them—but once you get the hang of it, it almost becomes second nature.
You can read more about it [here](get a link to a good resource).

The H5 “C++” API, on the other hand, is a terrifying, monstrous beast.
Finding resources for it online is next to impossible, it has some very unintuitive ways of doing things, has terrible runtime errors that are next to impossible to debug—and that sometimes have nothing to do with HDF5 itself—and overall, is just a C API with some classes thrown in.

Before, the code used to be copy-pasted.
(fig 1) Each writer function would create its own folder and write its data in an (annoyingly) slightly-different way.
Each update would have its own dataset inside those folders, which meant that compression was not very optimal.
Moreover, chunking was implemented on a 1:1 basis (one chunk per dataset) which meant that reading times were slow, too.
(table 1)

The first step was to refactor the code.
Initially, setup of the datasets was done on an individual basis.
This involved creating and opening a dataset, setting up the correct properties such as chunking and compression, writing the data, and closing the dataset.
 With a general template, implementing any future changes would involve changing just one function instead of twenty.

Knowing full well that we needed an extensible and reusable approach, this writer template was designed with the specific aim of being as generic as possible.
In an effort to abstract away as much of the API calls as possible, and to be able to use this logging framework in other projects, we also moved most of the infrastructure to its own class.

After extensive refactoring, we began to work on taking advantage of HDF5’s dataset compression the best we could.

Since HDF5 is only capable of doing intrachunk compression—that is, within the same chunk—our current method of writing one update per chunk would not suffice.
This is because, much like in the real world, in the digital world change happens slowly.
The state of the cells remains relatively stable from update to update, and evolution can only be appreciated when analysing a bigger timeframe.
Since there is not a lot of variation between updates, we have excellent compressibility.

In order to see how to progress, we conducted some trials to see what would be the best layout for updates within the chunks.
Four candidate layouts, as well as the original layout, were tested.
(fig 2)

| layout   | filesize  (MiB) |
|----------|----------------|
| original | 471            |
| X-wise   | 416            |
| Y-wise   | 417            |
| Z-wise   | 414            |
| 2D-wise  | 417            |

Since all four layouts showed an improvement over the original, and since they were all within the margin of error of each other, we decided to go with the most intuitive layout, in this case, Z-wise.

While seemingly small, a 12% improvement in filesize is nothing to laugh at—in fact, we could have simply stopped here.
However, the improvements we made to the file writing mechanism made it easier to implement further changes, so we decided to keep going.

Using a convenient utility, hdf5dump, we could get an overview of everything that was going on in the .h5 file without actually looking at the data.
Using a python script to deal with the weird dump format, we managed to extract the compression ratio and size of every single dataset.
With another script, we graphed these results.
(fig 3: graph of compression, fig 4: graph of filesize) It is clear that these “decoders” are what is now taking up most of the file.

But what is a decoder?

Simply put, a decoder is a map of something we care about (be them functions, regulators, etc) to UIDs of cells.
It is a neat way to keep track of relevant data without much overhead—or so we thought.
You see, in the original implementation, decoders were written to file as datasets of strings.
This was convenient—since HDF5 strings are easy to handle compared to the alternatives—interoperable—since any other program could just read the string—and human-readable—because, y’know, they are strings.
However, strings in general and HDF5 strings in particular have a lot of overhead.
We can do better.

Instead of saving a stringified interpretation of the decoders, we could just save the information the strings represent.
This involved dealing with HDF5 variable length arrays, as well as fixed-sized arrays.

For some of the decoders, we needed to store bitsets representing X.
Since “bitset” is not a type in the HDF5 world, we needed to find a replacement.
Luckily, the size of these bitsets is known at compile time, so we can effectively replace them with an H5 ArrayType of unsigned chars.
In the other decoders, ints sufficed.

While we could have simply stored the decoders (be them of int or ArrayType) directly in datasets, the information they contain is of variable length.
This meant that if an update n had m as many decoders as the ones prior, the dataset would have had to grow by m, in turn storing m(n-1) empty cells, which take up space.
This is unacceptable, so we instead chose to store the decoders inside VarLenTypes, arrays whose length can be changed during runtime.
(fig)

Saving the decoders in binary format gives us a file size gain of 45% over our previous results, bringing the full savings up to 52%.
This is fantastic.
 However, storing 16k updates (around 1h of experiments) still takes up 225MiB, which while less than the previous 471MiB, is still more than we’d like.
After all, experiments are generally run for weeks at a time, and at some point we have to get the results out of the HPC.

We fiddled around with different compression ratios (the zlib algorithm takes 0-9, with 0 being no compression and 9 being highest compression).
In an effort to reduce H5 overhead, as well as provide some interchunk compression, we also tried compressing the output files.
To our surprise, this resulted in a 50% smaller file size! The results can be seen on table X

All in all, after months of refactoring old code, studying and analysing a legacy API, and debugging esoteric error messages, the results speak for themselves.

Conclusions

* Talk about code line deletions
* Measure save time in original code
* Compress original output files
* Real-life HPCC use case
