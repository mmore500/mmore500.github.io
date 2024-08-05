---
layout: efflux
title: "Trackable Agent-based Evolution Models at Wafer Scale"
date: 2024-04-16
permalink: "/pubs/:title"
category: conference
doi: 10.1162/isal_a_00830
download: https://direct.mit.edu/isal/proceedings-pdf/isal2024/36/87/2461093/isal_a_00830.pdf
view_publisher: https://doi.org/10.1162/isal_a_00830
authors:
  - Matthew Andres Moreno
  - Connor Yang
  - Emily Dolson
  - Luis Zaman
venue: The 2024 Conference on Artificial Life
projects:
  - hstrat
  - conduit
abstract: |
  Continuing improvements in computing hardware are poised to transform capabilities for in silico modeling of cross-scale phenomena underlying major open questions in evolutionary biology and artificial life, such as transitions in individuality, eco-evolutionary dynamics, and rare evolutionary events.
  Emerging ML/AI-oriented hardware accelerators, like the 850,000 processor Cerebras Wafer Scale Engine (WSE), hold particular promise.
  However, practical challenges remain in conducting informative evolution experiments that efficiently utilize these platforms' large processor counts.
  Here, we focus on the problem of extracting phylogenetic information from agent-based evolution on the WSE platform.
  This goal drove significant refinements to decentralized in silico phylogenetic tracking, reported here.
  These improvements yield order-of-magnitude performance improvements.
  We also present an asynchronous island-based genetic algorithm (GA) framework for WSE hardware.
  Emulated and on-hardware GA benchmarks with a simple tracking-enabled agent model clock upwards of 1 million generations a minute for population sizes reaching 16 million agents.
  We validate phylogenetic reconstructions from these trials and demonstrate their suitability for inference of underlying evolutionary conditions.
  In particular, we demonstrate extraction, from wafer-scale simulation, of clear phylometric signals that differentiate runs with adaptive dynamics enabled versus disabled.
  Together, these benchmark and validation trials reflect strong potential for highly scalable agent-based evolution simulation that is both efficient and observable.
  Developed capabilities will bring entirely new classes of previously intractable research questions within reach, benefiting further explorations within the evolutionary biology and artificial life communities across a variety of emerging high-performance computing platforms.
bibtex: |-
  @inproceedings{moreno2024trackable,
    author={Matthew Andres Moreno and Connor Yang and Emily Dolson and Luis Zaman},
    title = {Trackable Agent-based Evolution Models at Wafer Scale},
    booktitle = {The 2024 Conference on Artificial Life},
    collection = {ALIFE 2024},
    publisher = {MIT Press},
    year = {2024},
    month = {07},
    doi={10.1162/isal_a_00830},
    url={https://doi.org/10.1162/isal_a_00830},
    numpages={12},
    pages={87-98},
  }
citation:  'Moreno, M. A., Yang, C., Dolson, E., & Zaman, L. (2024). Trackable Agent-based Evolution Models at Wafer Scale. In The 2024 Conference on Artificial Life. MIT Press. https://doi.org/10.1162/isal_a_00830'
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/hstrat-wafer-scale/tree/v0.2.0) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [kernel software](https://github.com/mmore500/wse-sketches) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [data](https://osf.io/bfm2z/) [via Open Science Framework ❋](https://osf.io)
  - [conference slides](https://docs.google.com/presentation/d/1mxOdbO7nnWkTjid5wmuwV3dqEa9O1T1DtcxRuxlsQSE) [via Google Slides](https://workspace.google.com/products/slides/)
---
