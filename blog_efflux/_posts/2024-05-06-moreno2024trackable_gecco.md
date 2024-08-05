---
layout: efflux
title: "Trackable Island-model Genetic Algorithms at Wafer Scale"
date: 2024-05-06
permalink: "/pubs/:title"
category: abstract
doi: 10.1145/3638530.3664090
download: https://dl.acm.org/doi/pdf/10.1145/3638530.3664090
view_publisher: https://doi.org/10.1145/3638530.3664090
authors:
  - Matthew Andres Moreno
  - Connor Yang
  - Emily Dolson
  - Luis Zaman
venue: The Genetic and Evolutionary Computation Conference
projects:
  - hstrat
  - conduit
abstract: |
  Emerging ML/AI hardware accelerators, like the 850,000 processor Cerebras Wafer-Scale Engine (WSE), hold great promise to scale up the capabilities of evolutionary computation.
  However, challenges remain in maintaining visibility into underlying evolutionary processes while efficiently utilizing these platforms’ large processor counts.
  Here, we focus on the problem of extracting phylogenetic information from digital evolution on the WSE platform.
  We present a tracking-enabled asynchronous island-based genetic algorithm (GA) framework for WSE hardware.
  Emulated and on-hardware GA benchmarks with a simple tracking-enabled agent model clock upwards of 1 million generations a minute for population sizes reaching 16 million.
  This pace enables quadrillions of evaluations a day.
  We validate phylogenetic reconstructions from these trials and demonstrate their suitability for inference of underlying evolutionary conditions.
  In particular, we demonstrate extraction of clear phylometric signals that differentiate wafer-scale runs with adaptive dynamics enabled versus disabled.
  Together, these benchmark and validation trials reflect strong potential for highly scalable evolutionary computation that is both efficient and observable.
  Kernel code implementing the island-model GA supports drop-in customization to support any fixed-length genome content and fitness criteria, allowing it to be leveraged to advance research interests across the community.

bibtex: |-
  @inproceedings{moreno2024trackable_gecco,
    author={Matthew Andres Moreno and Connor Yang and Emily Dolson and Luis Zaman},
    title = {Trackable Island-model Genetic Algorithms at Wafer Scale},
    pages = {101-102},
    isbn = {9798400704956},
    year = {2024},
    publisher= {Association for Computing Machinery},
    address = {New York, NY, USA},
    url = {https://doi.org/10.1145/3638530.3664090},
    doi = {10.1145/3638530.3664090},
    booktitle= {Proceedings of the Genetic and Evolutionary Computation Conference Companion},
    numpages = {2},
    location = {Melbourne, VIC, Australia},
    series = {GECCO '24}
  }
citation: "Matthew Andres Moreno, Connor Yang, Emily Dolson, and Luis Zaman. 2024. Trackable Island-model Genetic Algorithms at Wafer Scale. In Proceedings of the Companion Conference on Genetic and Evolutionary Computation (GECCO '24 Companion). Association for Computing Machinery, New York, NY, USA. https://doi.org/10.1145/3638530.3664090"
supporting_materials: |
  - [LaTeX source](https://github.com/mmore500/hstrat-wafer-scale/tree/tex-extended-abstract) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [primary publication](https://doi.org/10.48550/arXiv.2404.10861)
---
