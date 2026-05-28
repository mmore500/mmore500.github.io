---
layout: efflux
title: "PhyloFrame: A DataFrame-based Library for Fast, Flexible Phylogenetic Computation"
date: 2026-05-27
permalink: "/pubs/:title"
category: preprint
doi: 10.48550/arXiv.2605.28545
download: https://arxiv.org/pdf/2605.28545.pdf
view_publisher: https://doi.org/10.48550/arXiv.2605.28545
authors:
  - Matthew Andres Moreno
  - Jeet Sukumaran
  - Luis Zaman
  - Emily Dolson
venue: arXiv
projects:
  - libraries
abstract: |
  PhyloFrame is a Python library for phylogenetic computation targeting the gap between specialist, compiler-optimized operations and flexible, script-based workflows -- with emphasis on fast, memory-efficient operations for very large tree sizes (e.g., ≥ 300,000 taxa).
  PhyloFrame is built around a DataFrame-based tree representation, where each row corresponds to a node and columns record ancestor relationships, branch lengths, taxon labels, and any user-defined attributes.
  Crucial for scalability, such array-backed storage allows both library and end-user code alike to seamlessly harness Just-in-Time (JIT) compilation (e.g., Numba) and vectorized execution (e.g., NumPy, Polars).
  At large tree sizes, performance generally matches or exceeds Python libraries backed by native code -- notably, achieving strong performance in topological-order traversals and Newick I/O.
bibtex: |-
  @misc{moreno2026phyloframe,
        doi={10.48550/arXiv.2605.28545},
        url={https://arxiv.org/abs/2605.28545},
        title={PhyloFrame: A DataFrame-based Library for Fast, Flexible Phylogenetic Computation},
        author={Matthew Andres Moreno and Jeet Sukumaran and Luis Zaman and Emily Dolson},
        year={2026},
        eprint={2605.28545},
        archivePrefix={arXiv},
        primaryClass={q-bio.PE},
  }
citation: "Moreno M. A., Sukumaran J., Zaman L., & Dolson E. (2026). PhyloFrame: A DataFrame-based Library for Fast, Flexible Phylogenetic Computation. arXiv preprint arXiv:2605.28545. https://doi.org/10.48550/arXiv.2605.28545"
supporting_materials: |
  - [software repository](https://github.com/mmore500/phyloframe) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software package](https://pypi.org/project/phyloframe/) [via PyPI](https://pypi.org/)
  - [documentation](https://phyloframe.readthedocs.io) [via Read the Docs](https://readthedocs.org/)
---
