---
layout: efflux
title: "Hereditary stratigraphy: genome annotations to enable phylogenetic inference over distributed populations"
date: 2022-05-13
category: abstract
download: https://github.com/mmore500/hereditary-stratigraph-concept/releases/download/v0.2.0/hereditary-stratigraph-concept.pdf
view_publisher: https://doi.org/10.1145/3520304.3533937
doi: "10.1145/3520304.3533937"
authors:
  - Matthew Andres Moreno
  - Emily Dolson
  - Charles Ofria
venue: The Genetic and Evolutionary Computation Conference
abstract: |
  Phylogenetic analyses can also enable insight into evolutionary and ecological dynamics such as selection pressure and frequency dependent selection in digital evolution systems.
  Traditionally digital evolution systems have recorded data for phylogenetic analyses through perfect tracking where each birth event is recorded in a centralized data structures.
  This approach, however, does not easily scale to distributed computing environments where evolutionary individuals may migrate between a large number of disjoint processing elements.
  To provide for phylogenetic analyses in these environments, we propose an approach to infer phylogenies via heritable genetic annotations rather than directly track them. We introduce a "hereditary stratigraphy" algorithm that enables efficient, accurate phylogenetic reconstruction with tunable, explicit trade-offs between annotation memory footprint and reconstruction accuracy.
  This approach can estimate, for example, MRCA generation of two genomes within 10% relative error with 95% confidence up to a depth of a trillion generations with genome annotations smaller than a kilobyte.
  We also simulate inference over known lineages, recovering up to 85.70% of the information contained in the original tree using a 64-bit annotation.
bibtex: |-
  @inproceedings{moreno2022hereditary_gecco,
    author = {Moreno, Matthew Andres and Dolson, Emily and Ofria, Charles},
    title = {Hereditary Stratigraphy: Genome Annotations to Enable Phylogenetic Inference over Distributed Populations},
    year = {2022},
    isbn = {9781450392686},
    publisher = {Association for Computing Machinery},
    address = {New York, NY, USA},
    url = {https://doi.org/10.1145/3520304.3533937},
    doi = {10.1145/3520304.3533937},
    booktitle = {Proceedings of the Genetic and Evolutionary Computation Conference Companion},
    pages = {65–66},
    numpages = {2},
    keywords = {phylogenetics, decentralized algorithms, genetic algorithms, digital evolution, genetic programming},
    location = {Boston, Massachusetts},
    series = {GECCO '22}
  }
citation: "Matthew Andres Moreno, Emily Dolson, and Charles Ofria. 2022. Hereditary stratigraphy: genome annotations to enable phylogenetic inference over distributed populations. In Proceedings of the Genetic and Evolutionary Computation Conference Companion (GECCO '22). Association for Computing Machinery, New York, NY, USA, 65–66. https://doi.org/10.1145/3520304.3533937"
supporting_materials: |
  - [data](https://osf.io/4sm72/) [via Open Science Framework ❋](https://osf.io)
  - [source code](https://github.com/mmore500/hereditary-stratigraph-concept/tree/v0.2.0) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [hstrat library code](https://github.com/mmore500/hstrat/tree/v0.3.2) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [web demo 1](https://hopth.ru/bh)
  - [web demo 2](https://hopth.ru/bi)
  - [presentation](https://www.youtu.be/-lf3NdcKOZ2c) [via YouTube <i class="icon-video"></i>](https://youtube.com)
  - [poster](https://docs.google.com/presentation/d/13Lfm8Xj0Pdd_PNWCFZlIgjlz4cZT7Ph91-tMlX7VhL0) [via Google Slides](https://workspace.google.com/products/slides/)
  - [slides](https://docs.google.com/presentation/d/1MTTIXU-ddJ83NF02qdqycIUwZKEt-Tc4CG_0Te6bVdA) [via Google Slides](https://workspace.google.com/products/slides/)
  - [LaTeX source](https://github.com/mmore500/hereditary-stratigraph-concept/tree/v0.2.0) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
