---
layout: efflux
title: "Trackable Island-model Genetic Algorithms at Wafer Scale"
date: 2024-11-16
permalink: "/pubs/:title"
category: abstract
download: https://sc24.supercomputing.org/proceedings/poster/poster_files/post166s2-file2.pdf
view_publisher: https://sc24.supercomputing.org/proceedings/poster/poster_pages/post166.html
authors:
  - Matthew Andres Moreno
  - Connor Yang
  - Emily Dolson
  - Luis Zaman
venue: The International Conference for High Performance Computing, Networking, Storage, and Analysis (SC24)
projects:
  - hstrat
abstract: |
   Emerging ML/AI hardware accelerators, like the 850,000 processor Cerebras Wafer-Scale Engine (WSE), hold great promise to scale up the capabilities of evolutionary computation.
   However, challenges remain in maintaining visibility into underlying evolutionary processes while efficiently utilizing these platforms' large processor counts.
   Here, we focus on the problem of extracting phylogenetic history. We present a tracking-enabled asynchronous island-based genetic algorithm (GA) framework for WSE hardware.
   Emulated and on-hardware GA benchmarks with a simple tracking-enabled agent model clock upwards of 1 million generations per minute for population sizes reaching 16 million.
   We validate phylogenetic reconstructions from these trials and demonstrate their suitability for inference of underlying evolutionary conditions.
   In particular, we demonstrate extraction of clear phylometric signals that differentiate adaptive dynamics.
   Kernel code implementing the island-model GA supports drop-in customization to support any fixed-length genome content and fitness criteria, benefiting further explorations within the evolutionary biology and evolutionary computation communities.
bibtex: |-
  @inproceedings{moreno2024trackable_sc,
    author = {Matthew Andres Moreno and Connor Yang and Emily Dolson and Luis Zaman},
    title = {Trackable Agent-Based Evolution Models at Wafer Scale},
    year = {2024},
    url = {https://sc24.supercomputing.org/proceedings/poster/poster_pages/post166.html},
    booktitle = {SC24 Research Poster and ACM Student Research Competition Poster Archive},
    numpages = {2},
    location = {Atlanta, Georgia}
  }
citation: "Matthew Andres Moreno, Connor Yang, Emily Dolson, and Luis Zaman. 2024. Trackable Agent-Based Evolution Models at Wafer Scale. In SC24 Research Poster and ACM Student Research Competition Poster Archive. https://sc24.supercomputing.org/proceedings/poster/poster_pages/post166.html"
supporting_materials: |
  - [LaTeX source](https://github.com/mmore500/hstrat-wafer-scale/tree/tex-extended-abstract) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [primary publication](https://doi.org/10.48550/arXiv.2404.10861)
  - [poster](https://sc24.supercomputing.org/proceedings/poster/poster_files/post166s2-file2.pdf)
---
