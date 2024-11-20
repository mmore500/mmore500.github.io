---
layout: efflux
title: "Analysis of Phylogeny Tracking Algorithms for Serial and Multiprocess Applications"
date: 2024-03-03
permalink: "/pubs/:title"
category: preprint
doi: 10.48550/arXiv.2403.00246
download: https://arxiv.org/pdf/2403.00246.pdf
view_publisher: https://doi.org/10.48550/arXiv.2403.00246
authors:
  - Matthew Andres Moreno
  - Santiago Rodriguez Papa
  - Emily Dolson
venue: arXiv
projects:
  - hstrat
abstract: |
  Since the advent of modern bioinformatics, the challenging, multifaceted problem of reconstructing phylogenetic history from biological sequences has hatched perennial statistical and algorithmic innovation.
  Studies of the phylogenetic dynamics of digital, agent-based evolutionary models motivate a peculiar converse question: how to best engineer tracking to facilitate fast, accurate, and memory-efficient lineage reconstructions?
  Here, we formally describe procedures for phylogenetic analysis in both serial and distributed computing scenarios.
  With respect to the former, we demonstrate reference-counting-based pruning of extinct lineages.
  For the latter, we introduce a trie-based phylogenetic reconstruction approach for "hereditary stratigraphy" genome annotations.
  This process allows phylogenetic relationships between genomes to be inferred by comparing their similarities, akin to reconstruction of natural history from biological DNA sequences.
  Phylogenetic analysis capabilities significantly advance distributed agent-based simulations as a tool for evolutionary research, and also benefit application-oriented evolutionary computing.
  Such tracing could extend also to other digital artifacts that proliferate through replication, like digital media and computer viruses.
bibtex: |-
  @misc{moreno2024analysis,
        doi={10.48550/arXiv.2403.00246},
        url={https://arxiv.org/abs/2403.00246},
        title={Analysis of Phylogeny Tracking Algorithms for Serial and Multiprocess Applications},
        author={Matthew Andres Moreno and Santiago {Rodriguez Papa} and Emily Dolson},
        year={2024},
        eprint={2403.00246},
        archivePrefix={arXiv},
        primaryClass={cs.DS}
  }
citation: "Moreno, M. A., Rodriguez Papa, S., & Dolson, E. (2024). Analysis of Phylogeny Tracking Algorithms for Serial and Multiprocess Applications. arXiv preprint arXiv:2403.00246 https://doi.org/10.48550/arXiv.2403.00246"
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/phylotrack-algorithm-analysis) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
