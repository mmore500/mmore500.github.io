---
layout: efflux
title: "A Scalable Trie Building Algorithm for High-Throughput Phyloanalysis of Wafer-Scale Digital Evolution Experiments"
date: 2025-08-20
permalink: "/pubs/:title"
category: conference
doi: 10.48550/arXiv.2508.15074
download: https://arxiv.org/pdf/2508.15074
view_publisher: https://arxiv.org/abs/2508.15074
authors:
  - Vivaan Singhvi
  - Joey Wagner
  - Emily Dolson
  - Luis Zaman
  - Matthew Andres Moreno
venue: The 2025 Conference on Artificial Life
projects:
  - hstrat
abstract: |
  Agent-based simulation platforms play a key role in enabling fast-to-run evolution experiments that can be precisely controlled and observed in detail.
  Availability of high-resolution snapshots of lineage ancestries from digital experiments, in particular, is key to investigations of evolvability and open-ended evolution, as well as in providing a validation testbed for bioinformatics method development.
  Ongoing advances in AI/ML hardware accelerator devices, such as the 850,000-processor Cerebras Wafer-Scale Engine (WSE), are poised to broaden the scope of evolutionary questions that can be investigated \textit{in silico}.
  However, constraints in memory capacity and locality characteristic of these systems introduce difficulties in exhaustively tracking phylogenies at runtime.
  To overcome these challenges, recent work on hereditary stratigraphy algorithms has developed space-efficient genetic markers to facilitate fully decentralized estimation of relatedness among digital organisms.
  However, in existing work, compute time to reconstruct phylogenies from these genetic markers has proven a limiting factor in achieving large-scale phyloanalyses.
  Here, we detail an improved trie-building algorithm designed to produce reconstructions equivalent to existing approaches.
  For modestly-sized 10,000-tip trees, the proposed approach achieves a 300-fold speedup versus existing state-of-the-art.
  Finally, using 1 billion genome datasets drawn from WSE simulations encompassing 954 trillion replication events, we report a pair of large-scale phylogeny reconstruction trials, achieving end-to-end reconstruction times of 2.6 and 2.9 hours.
  In substantially improving reconstruction scaling and throughput, presented work establishes a key foundation to enable powerful high-throughput phyloanalysis techniques in large-scale digital evolution experiments.
bibtex: |-
  @inproceedings{singhvi2025scalable,
    author = {Vivaan Singhvi and Joey Wagner and Emily Dolson and Luis Zaman and Matthew Andres Moreno},
    title = {A Scalable Trie Building Algorithm for High-Throughput Phyloanalysis of Wafer-Scale Digital Evolution Experiments},
    booktitle = {The 2025 Conference on Artificial Life},
    collection = {ALIFE 2025},
    publisher = {MIT Press},
    year = {in press},
    doi={10.48550/arXiv.2508.15074},
    url={https://doi.org/10.48550/arXiv.2508.15074},
    month = {10},
    numpages={12},
  }
citation:  'Singhvi, V., Wagner, J., Dolson, E., Zaman, L., & Moreno, M. A. (in press). "A Scalable Trie Building Algorithm for High-Throughput Phyloanalysis of Wafer-Scale Digital Evolution Experiments. In The 2025 Conference on Artificial Life. MIT Press. https://doi.org/10.48550/arXiv.2508.15074'
supporting_materials: |
  - [manuscript, notebooks, and scripts source](https://github.com/mmore500/hstrat-reconstruction-algo/tree/v1.1.1) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [manuscript, notebooks, and scripts archive](https://doi.org/10.5281/zenodo.16898918) [via Zenodo *z*](https://zenodo.org)
  - [WSE kernel source](https://github.com/mmore500/wse-async-ga/tree/v2025.12.26) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [WSE kernel archive](https://doi.org/10.5281/zenodo.16898904) [via Zenodo *z*](https://zenodo.org)
  - [hstrat source](https://github.com/mmore500/hstrat/tree/v1.20.10) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [hstrat archive](https://doi.org/10.5281/zenodo.16898849) [via Zenodo *z*](https://zenodo.org)
  - [supplement](https://osf.io/5q9ra) [via Open Science Framework ❋](https://osf.io)
  - [data](https://osf.io/63ucz) [via Open Science Framework ❋](https://osf.io)
  - [conference poster](https://docs.google.com/presentation/d/1sZqgj76n7Ms_QyGwkytiCPM8q7xpJ7Bfdq6BY1-XiD0) [via Google Slides](https://workspace.google.com/products/slides/)
---
