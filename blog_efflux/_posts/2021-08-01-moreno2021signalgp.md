---
layout: efflux
title: "SignalGP-Lite: Event Driven Genetic Programming Library for Large-Scale Artificial Life Applications "
date: 2022-08-01
permalink: "/pubs/:title"
category: preprint
download: https://arxiv.org/pdf/2108.00382
view_publisher: https://doi.org/10.48550/arXiv.2108.00382
doi: 10.48550/arXiv.2108.00382
authors:
  - Matthew Andres Moreno
  - Santiago Rodriguez Papa
  - Alexander Lalejini
  - Charles Ofria
venue: arXiv
projects:
  - software
abstract: |
  Developing software to effectively take advantage of growth in parallel and distributed processing capacity poses significant challenges.
  Traditional programming techniques allow a user to assume that execution, message passing, and memory are always kept synchronized.
  However, maintaining this consistency becomes increasingly costly at scale.
  One proposed strategy is "best-effort computing", which relaxes synchronization and hardware reliability requirements, accepting nondeterminism in exchange for efficiency.
  Although many programming languages and frameworks aim to facilitate software development for high performance applications, existing tools do not directly provide a prepackaged best-effort interface.
  The Conduit C++ Library aims to provide such an interface for convenient implementation of software that uses best-effort inter-thread and inter-process communication.
  Here, we describe the motivation, objectives, design, and implementation of the library.
  Benchmarks on a communication-intensive graph coloring problem and a compute-intensive digital evolution simulation show that Conduit's best-effort model can improve scaling efficiency and solution quality, particularly in a distributed, multi-node context.
bibtex: |-
  @misc{moreno2021signalgp,
    doi = {10.48550/ARXIV.2108.00382},

    url = {https://arxiv.org/abs/2108.00382},

    author = {Moreno, Matthew Andres and {Rodriguez Papa}, Santiago and Lalejini, Alexander and Ofria, Charles},

    keywords = {Neural and Evolutionary Computing (cs.NE), FOS: Computer and information sciences, FOS: Computer and information sciences},

    title = {SignalGP-Lite: Event Driven Genetic Programming Library for Large-Scale Artificial Life Applications},

    publisher = {arXiv},

    year = {2021},

    copyright = {arXiv.org perpetual, non-exclusive license}
  }
citation: "Moreno, M. A., Rodriguez Papa, S., & Ofria, C. (2021). SignalGP-Lite: Event Driven Genetic Programming Library for Large-Scale Artificial Life Applications. arXiv preprint arXiv:2108.00382."
supporting_materials: |
  - [data](https://osf.io/7jkgp/) [via Open Science Framework ❋](https://osf.io)
  - [source code](https://github.com/mmore500/signalgp-lite) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [slides](https://docs.google.com/presentation/d/1VkqDi7xSG63mFnS-Ox6C4Nel6uS5AvTQB9r9kKnSS0o/) [via Google Slides](https://workspace.google.com/products/slides/)
---
