---
layout: efflux
title: "Testing the Inference Accuracy of Accelerator-friendly Approximate Phylogeny Tracking"
date: 2024-12-05
permalink: "/pubs/:title"
category: conference
download: https://github.com/mmore500/hstrat-reconstruction-quality/releases/download/v1.0.0/hstrat-reconstruction-quality.pdf
authors:
  - Matthew Andres Moreno
  - Anika Ranjan
  - Emily Dolson
  - Luis Zaman
venue: 2025 IEEE Symposium on Computational Intelligence in Artificial Life and Cooperative Intelligent Systems
projects:
  - hstrat
abstract: |
  Computer simulations are an important tool for studying the mechanics of biological evolution.
  In particular, agent-based approaches provide an opportunity to collect high-quality records of ancestry relationships.
  Such phylogenies can provide insight into evolutionary dynamics within these simulations.
  Previous work generally tracks lineages directly, yielding an exact phylogenetic record of evolutionary history.
  However, challenges exist in scaling direct ancestry-tracking approaches to highly-distributed, many-processor evolution *in silico*.
  An alternative approach is to estimate phylogenetic history via non-coding annotations on digital genomes, akin to how bioinformaticians build phylogenies by assessing genetic similarities between organisms.
  Recent work has extended this "hereditary stratigraphy" approach to support powerful hardware accelerator platforms, such as the Cerebras Wafer-Scale Engine.
  Although these second-generation "surface"-based hereditary stratigraphy algorithms have demonstrated order-of-magnitude speedups over first-generation "column"-based algorithms, it remains unknown how they impact the accuracy of reconstructed phylogenies.
  To address this question, we assessed reconstruction accuracy under alternative configurations across a matrix of evolutionary conditions varying in selection pressure, spatial structure, and ecological dynamics.
  Encouragingly, we find that the second-generation approaches provide higher reconstruction quality across most surveyed conditions.
bibtex: |-
  @inproceedings{moreno2025testing,
    title = {Testing the Inference Accuracy of Accelerator-friendly Approximate Phylogeny Tracking},
    author=  {Matthew Andres Moreno and Anika Ranjan and Emily Dolson and Luis Zaman},
    booktitle = {2025 IEEE Symposium on Computational Intelligence in Artificial Life and Cooperative Intelligent Systems},
    location = {Trondheim, Norway},
    publisher = {IEEE},
    address = {Piscataway, NJ, USA},
    year={in press},
  }
citation: "Moreno, M. A., Ranjan, A., Dolson, E., & Zaman, L. (in press). In The 2025 IEEE Symposium on Computational Intelligence in Artificial Life and Cooperative Intelligent Systems. IEEE."
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/hstrat-reconstruction-quality/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [code and notebooks](https://github.com/mmore500/hstrat-reconstruction-quality/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [data](https://osf.io/vqe7b/) [via Open Science Framework ❋](https://osf.io)
---
