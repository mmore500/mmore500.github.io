---
layout: efflux
title: "Testing the Inference Accuracy of Accelerator-friendly Approximate Phylogeny Tracking"
date: 2024-12-05
permalink: "/pubs/:title"
category: conference
download: https://github.com/mmore500/hstrat-reconstruction-quality/releases/download/v1.1.0/2024390545.pdf
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
    author={Moreno, Matthew Andres and Ranjan, Anika and Dolson, Emily and Zaman, Luis},
    booktitle={2025 IEEE Symposium on Computational Intelligence in Artificial Life and Cooperative Intelligent Systems (ALIFE-CIS)},
    title={Testing the Inference Accuracy of Accelerator-Friendly Approximate Phylogeny Tracking},
    year={2025},
    pages={1-9},
    location = {Trondheim, Norway},
    publisher = {IEEE},
    address = {Piscataway, NJ, USA},
    doi={10.1109/ALIFE-CIS64968.2025.10979833},
    url={https://doi.org/10.1109/ALIFE-CIS64968.2025.10979833}
  }
citation: 'M. A. Moreno, A. Ranjan, E. Dolson and L. Zaman, "Testing the Inference Accuracy of Accelerator-Friendly Approximate Phylogeny Tracking," 2025 IEEE Symposium on Computational Intelligence in Artificial Life and Cooperative Intelligent Systems (ALIFE-CIS), Trondheim, Norway, 2025, pp. 1-9, doi: 10.1109/ALIFE-CIS64968.2025.10979833.'
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/hstrat-reconstruction-quality/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [code and notebooks](https://github.com/mmore500/hstrat-reconstruction-quality/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [data](https://osf.io/vqe7b/) [via Open Science Framework ❋](https://osf.io)
  - [conference slides](https://docs.google.com/presentation/d/1XM_1cvXs6pVYpKzuTeSV8r_rLwNHncmAg3Jye4AjcjA) [via Google Slides](https://workspace.google.com/products/slides/)
  - [conference poster](https://docs.google.com/presentation/d/1k64iKqZsmsxi7gqmG1uR_9eLlG5M-T-sg5AJ0ras5cY) [via Google Slides](https://workspace.google.com/products/slides/)
---
