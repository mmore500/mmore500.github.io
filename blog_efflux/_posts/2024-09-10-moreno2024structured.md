---
layout: efflux
title: "Structured Downsampling for Fast, Memory-efficient Curation of Online Data Streams"
date: 2024-09-10
permalink: "/pubs/:title"
category: preprint
doi: 10.48550/arXiv.2409.06199
download: https://arxiv.org/pdf/2409.06199.pdf
view_publisher: https://doi.org/10.48550/arXiv.2409.06199
authors:
  - Matthew Andres Moreno
  - Luis Zaman
  - Emily Dolson
venue: arXiv
projects:
  - hstrat
  - libraries
abstract: |
  Operations over data streams typically hinge on efficient mechanisms to aggregate or summarize history on a rolling basis.
  For high-volume data steams, it is critical to manage state in a manner that is fast and memory efficient --- particularly in resource-constrained or real-time contexts.
  Here, we address the problem of extracting a fixed-capacity, rolling subsample from a data stream.
  Specifically, we explore "data stream curation" strategies to fulfill requirements on the composition of sample time points retained.
  Our "DStream" suite of algorithms targets three temporal coverage criteria: (1) steady coverage, where retained samples should spread evenly across elapsed data stream history; (2) stretched coverage, where early data items should be proportionally favored; and (3) tilted coverage, where recent data items should be proportionally favored.
  For each algorithm, we prove worst-case bounds on rolling coverage quality.
  We focus on the more practical, application-driven case of maximizing coverage quality given a fixed memory capacity.
  As a core simplifying assumption, we restrict algorithm design to a single update operation: writing from the data stream to a calculated buffer site --- with data never being read back, no metadata stored (e.g., sample timestamps), and data eviction occurring only implicitly via overwrite.
  Drawing only on primitive, low-level operations and ensuring full, overhead-free use of available memory, this "DStream" framework ideally suits domains that are resource-constrained, performance-critical, and fine-grained (e.g., individual data items as small as single bits or bytes).
  The proposed approach supports O(1) data ingestion via concise bit-level operations.
  To further practical applications, we provide plug-and-play open-source implementations targeting both scripted and compiled application domains.

bibtex: |-
  @misc{moreno2024structured,
        doi={10.48550/arXiv.2409.06199},
        url={https://arxiv.org/abs/2409.06199},
        title={Structured Downsampling for Fast, Memory-efficient Curation of Online Data Streams},
        author={Matthew Andres Moreno and Luis Zaman and Emily Dolson},
        year={2024},
        eprint={2409.06199},
        archivePrefix={arXiv},
        primaryClass={cs.DS}
  }
citation: "Moreno M. A., Zaman L., & Dolson E. (2024). Structured Downsampling for Fast, Memory-efficient Curation of Online Data Streams. arXiv preprint arXiv:2409.06199. https://doi.org/10.48550/arXiv.2409.06199"
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/hstrat-surface-concept/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software repository](https://github.com/mmore500/downstream/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software package](https://pypi.org/project/downstream/) [via PyPI](https://pypi.org/)
---
