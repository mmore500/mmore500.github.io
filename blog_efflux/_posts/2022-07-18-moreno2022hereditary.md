---
layout: efflux
title: "Hereditary stratigraphy: genome annotations to enable phylogenetic inference over distributed populations"
date: 2022-05-13
category: conference
download: https://github.com/mmore500/hereditary-stratigraph-concept/releases/download/v0.3.0/hereditary-stratigraph-concept-manuscript.pdf
view_publisher: https://doi.org/10.1162/isal_a_00550
doi: "10.1162/isal_a_00550"
authors:
  - Matthew Andres Moreno
  - Emily Dolson
  - Charles Ofria
venue: The 2022 Conference on Artificial Life
projects:
  - hstrat
abstract: |
  Phylogenies provide direct accounts of the evolutionary trajectories behind evolved artifacts in genetic algorithm and artificial life systems.
  Phylogenetic analyses can also enable insight into evolutionary and ecological dynamics such as selection pressure and frequency-dependent selection.
  Traditionally, digital evolution systems have recorded data for phylogenetic analyses through perfect tracking where each birth event is recorded in a centralized data structure.
  This approach, however, does not easily scale to distributed computing environments where evolutionary individuals may migrate between a large number of disjoint processing elements.
  To provide for phylogenetic analyses in these environments, we propose an approach to enable phylogenies to be inferred via heritable genetic annotations rather than directly tracked.
  We introduce a “hereditary stratigraphy” algorithm that enables efficient, accurate phylogenetic reconstruction with tunable, explicit trade-offs between annotation memory footprint and reconstruction accuracy.
  In particular, we demonstrate an approach that enables estimation of the most recent common ancestor (MRCA) between two individuals with fixed relative accuracy irrespective of lineage depth while only requiring logarithmic annotation space complexity with respect to lineage depth
  This approach can estimate, for example, MRCA generation of two genomes within 10% relative error with 95% confidence up to a depth of a trillion generations with genome annotations smaller than a kilobyte.
  We also simulate inference over known lineages, recovering up to 85.70% of the information contained in the original tree using 64-bit annotations.
bibtex: |-
  @proceedings{moreno2022hereditary,
      author = {Moreno, Matthew Andres and Dolson, Emily and Ofria, Charles},
      title = "{Hereditary Stratigraphy: Genome Annotations to Enable Phylogenetic Inference over Distributed Populations}",
      volume = {ALIFE 2022: The 2022 Conference on Artificial Life},
      series = {ALIFE 2022: The 2022 Conference on Artificial Life},
      year = {2022},
      month = {07},
      doi = {10.1162/isal_a_00550},
      url = {https://doi.org/10.1162/isal\_a\_00550},
      note = {64},
      eprint = {https://direct.mit.edu/isal/proceedings-pdf/isal/34/64/2035363/isal\_a\_00550.pdf},
  }
citation: 'Matthew Andres Moreno, Emily Dolson, Charles Ofria; July 18–22, 2022. "Hereditary Stratigraphy: Genome Annotations to Enable Phylogenetic Inference over Distributed Populations." Proceedings of the ALIFE 2022: The 2022 Conference on Artificial Life. ALIFE 2022: The 2022 Conference on Artificial Life. Online. (pp. 64). ASME. https://doi.org/10.1162/isal_a_00550'
supporting_materials: |
  - [data](https://osf.io/4sm72/) [via Open Science Framework ❋](https://osf.io)
  - [source code](https://github.com/mmore500/hereditary-stratigraph-concept/tree/v0.3.0) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [hstrat library code](https://github.com/mmore500/hstrat/tree/v0.3.2) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [web demo 1](https://hopth.ru/bh)
  - [web demo 2](https://hopth.ru/bi)
  - [presentation](https://www.youtu.be/-HJYNrafLpo) [via YouTube <i class="icon-video"></i>](https://youtube.com)
  - [slides](https://docs.google.com/presentation/d/1cHYcvigxfQnHAShV0wS4bZoV2_1BKOyGRFlejZCih3w/) [via Google Slides](https://workspace.google.com/products/slides/)
  - [LaTeX source](https://github.com/mmore500/hereditary-stratigraph-concept/tree/v0.3.0) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
