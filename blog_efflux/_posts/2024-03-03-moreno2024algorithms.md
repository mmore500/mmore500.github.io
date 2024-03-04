---
layout: efflux
title: "Algorithms for Efficient, Compact Online Data Stream Curation"
date: 2024-03-03
permalink: "/pubs/:title"
category: preprint
download: https://arxiv.org/pdf/2403.00266.pdf
view_publisher: https://arxiv.org/abs/2403.00266
authors:
  - Matthew Andres Moreno
  - Santiago Rodriguez Papa
  - Emily Dolson
venue: arXiv
projects:
  - hstrat
abstract: |
  Data stream algorithms tackle operations on high-volume sequences of read-once data items.
  Data stream scenarios include inherently real-time systems like sensor networks and financial markets.
  They also arise in purely-computational scenarios like ordered traversal of big data or long-running iterative simulations.
  In this work, we develop methods to maintain running archives of stream data that are temporally representative, a task we call "stream curation."
  Our approach contributes to rich existing literature on data stream binning, which we extend by providing stateless (i.e., non-iterative) curation schemes that enable key optimizations to trim archive storage overhead and streamline processing of incoming observations.
  We also broaden support to cover new trade-offs between curated archive size and temporal coverage.
  We present a suite of five stream curation algorithms that span O(n), O(logn), and O(1) orders of growth for retained data items.
  Within each order of growth, algorithms are provided to maintain even coverage across history or bias coverage toward more recent time points.
  More broadly, memory-efficient stream curation can boost the data stream mining capabilities of low-grade hardware in roles such as sensor nodes and data logging devices. 
bibtex: |-
  @misc{moreno2024algorithms,
        title={Algorithms for Efficient, Compact Online Data Stream Curation}, 
        author={Matthew Andres Moreno and Santiago Rodriguez Papa and Emily Dolson},
        year={2024},
        eprint={2403.00266},
        archivePrefix={arXiv},
        primaryClass={cs.DS}
  }
citation: "Moreno, M. A., Rodriguez Papa, S., & Dolson, E. (2024). Algorithms for Efficient, Compact Online Data Stream Curation. arXiv preprint arXiv:2403.00266."
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/hstrat-algo-analysis) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
