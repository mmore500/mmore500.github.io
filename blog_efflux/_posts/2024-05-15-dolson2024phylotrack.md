---
layout: efflux
title: "Phylotrack: C++ and Python libraries for in silico phylogenetic tracking"
date: 2024-05-15
permalink: "/pubs/:title"
category: preprint
doi: 10.48550/arXiv.2405.09389
download: https://arxiv.org/pdf/2405.09389.pdf
view_publisher: https://doi.org/10.48550/arXiv.2405.09389
authors:
  - Emily Dolson
  - Santiago Rodriguez-Papa
  - Matthew Andres Moreno
venue: arXiv
projects:
  - hstrat
abstract: |
  *In silico* evolution instantiates the processes of heredity, variation, and differential reproductive success (the three "ingredients" for evolution by natural selection) within digital populations of computational agents.
  Consequently, these populations undergo evolution, and can be used as virtual model systems for studying evolutionary dynamics.
  This experimental paradigm --- used across biological modeling, artificial life, and evolutionary computation --- complements research done using *in vitro* and *in vivo* systems by enabling experiments that would be impossible in the lab or field.
  One key benefit is complete, exact observability.
  For example, it is possible to perfectly record all parent-child relationships across simulation history, yielding complete phylogenies (ancestry trees).
  This information reveals when traits were gained or lost, and also facilitates inference of underlying evolutionary dynamics.

  The Phylotrack project provides libraries for tracking and analyzing phylogenies in *in silico* evolution.
  The project is composed of 1) Phylotracklib: a header-only C++ library, developed under the umbrella of the Empirical project, and 2) Phylotrackpy: a Python wrapper around Phylotracklib, created with Pybind11.
  Both components supply a public-facing API to attach phylogenetic tracking to digital evolution systems, as well as a stand-alone interface for measuring a variety of popular phylogenetic topology metrics.
  Underlying design and C++ implementation prioritizes efficiency, allowing for fast generational turnover for agent populations numbering in the tens of thousands.
  Several explicit features (e.g., phylogeny pruning and abstraction, etc.) are provided for reducing the memory footprint of phylogenetic information.
bibtex: |-
  @misc{dolson2024phylotrack,
        doi={10.48550/arXiv.2405.09389},
        url={https://arxiv.org/abs/2405.09389},
        title={Phylotrack: C++ and Python libraries for in silico phylogenetic tracking},
        author={Emily Dolson and Santiago Rodriguez-Papa and Matthew Andres Moreno},
        year={2024},
        eprint={2405.09389},
        archivePrefix={arXiv},
        primaryClass={q-bio.PE}
  }
citation: "Dolson, E., Rodriguez-Papa, S., & Moreno, M. A. (2024). Phylotrack: C++ and Python libraries for in silico phylogenetic tracking. arXiv preprint arXiv:2405.09389."
supporting_materials: |
  - [manuscript source](https://github.com/emilydolson/phylotrackpy/tree/5e5c219423f9e63be02e6a2dc1a64c186fa400e6/joss/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software repository](https://github.com/emilydolson/phylotrackpy/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software package](https://pypi.org/project/phylotrackpy/) [via PyPI <i class="icon-github-1"></i>](https://github.com/)
  - [data](https://osf.io/52hzs/) [via Open Science Framework ❋](https://osf.io)
---
