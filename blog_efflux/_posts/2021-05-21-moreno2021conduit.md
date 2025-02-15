---
layout: efflux
title: "Conduit: A C++ Library for Best-effort High Performance Computing"
date: 2021-05-21
permalink: "/pubs/:title"
category: workshop
download: https://github.com/mmore500/2021-gecco-conduit/releases/download/1.0.0/2021-gecco-conduit.pdf
view_publisher: https://doi.org/10.1145/3449726.3463205
doi: 10.1145/3449726.3463205
authors:
  - Matthew Andres Moreno
  - Santiago Rodriguez Papa
  - Charles Ofria
venue: ACM Workshop on Parallel and Distributed Evolutionary Inspired Methods
projects:
  - conduit
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
  @inproceedings{moreno2021conduit,
    author = {Moreno, Matthew Andres and Rodriguez Papa, Santiago and Ofria, Charles},
    title = {Conduit: A C++ Library for Best-Effort High Performance Computing},
    year = {2021},
    isbn = {9781450383516},
    publisher = {Association for Computing Machinery},
    address = {New York, NY, USA},
    url = {https://doi.org/10.1145/3449726.3463205},
    doi = {10.1145/3449726.3463205},
    booktitle = {Proceedings of the Genetic and Evolutionary Computation Conference Companion},
    pages = {1795–1800},
    numpages = {6},
    keywords = {high performance computing, best-effort computing},
    location = {Lille, France},
    series = {GECCO '21}
  }
citation: "Matthew Andres Moreno, Santiago {Rodriguez Papa}, and Charles Ofria. 2021. Conduit: a C++ library for best-effort high performance computing. In Proceedings of the Genetic and Evolutionary Computation Conference Companion (GECCO '21). Association for Computing Machinery, New York, NY, USA, 1795–1800. https://doi.org/10.1145/3449726.3463205"
supporting_materials: |
  - [data](https://osf.io/7jkgp/) [via Open Science Framework ❋](https://osf.io)
  - [interactive data notebooks](https://mybinder.org/v2/gh/mmore500/conduit/HEAD?filepath=binder%2F) [via MyBinder ❋](https://mybinder.org/)
  - [graph coloring benchmark source code](https://github.com/mmore500/conduit) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [digital evolution benchmark source code](https://github.com/mmore500/dishtiny) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [slides](https://docs.google.com/presentation/d/1iGgwiYkIzetOejq92ykxUcQFSLNCWzA65txObL2x0Sw) [via Google Slides](https://workspace.google.com/products/slides/)
  - [LaTeX source](https://github.com/mmore500/2021-gecco-conduit/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
