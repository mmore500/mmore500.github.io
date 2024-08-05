---
layout: efflux
title: "Runtime phylogenetic analysis enables extreme subsampling for test-based problems"
date: 2024-02-02
permalink: "/pubs/:title"
category: conference
download: https://dl.acm.org/doi/pdf/10.1145/3638530.3654208
view_publisher: https://doi.org/10.1145/3638530.3664090
doi: 10.1145/3638530.3664090
authors:
  - Alexander Lalejini
  - Marcos Sanson
  - Jack Garbus
  - Matthew Andres Moreno
  - Emily Dolson
venue: The Genetic and Evolutionary Computation Conference
projects:
abstract: |
  A phylogeny describes the evolutionary history of an evolving population.
  Evolutionary search algorithms can perfectly track the ancestry of candidate solutions, illuminating a population's trajectory through the search space.
  However, phylogenetic analyses are typically limited to post-hoc studies of search performance.
  We introduce phylogeny-informed subsampling, a new class of subsampling methods that exploit runtime phylogenetic analyses for solving test-based problems.
  Specifically, we assess two phylogeny-informed subsampling methods -- individualized random subsampling and ancestor-based subsampling -- on three diagnostic problems and ten genetic programming (GP) problems from program synthesis benchmark suites.
  Overall, we found that phylogeny-informed subsampling methods enable problem-solving success at extreme subsampling levels where other subsampling methods fail.
  For example, phylogeny-informed subsampling methods more reliably solved program synthesis problems when evaluating just one training case per-individual, per-generation.
  However, at moderate subsampling levels, phylogeny-informed subsampling generally performed no better than random subsampling on GP problems.
  Our diagnostic experiments show that phylogeny-informed subsampling improves diversity maintenance relative to random subsampling, but its effects on a selection scheme's capacity to rapidly exploit fitness gradients varied by selection scheme.
  Continued refinements of phylogeny-informed subsampling techniques offer a promising new direction for scaling up evolutionary systems to handle problems with many expensive-to-evaluate fitness criteria.
bibtex: |-
  @misc{lalejini2024runtime,
      doi = {10.1145/3638530.3664090},
      url = {https://doi.org/10.1145/3638530.3664090},
      isbn = {9798400704956},
      pages = {511–514},
      title={Runtime phylogenetic analysis enables extreme subsampling for test-based problems},
      author={Alexander Lalejini and Marcos Sanson and Jack Garbus and Matthew Andres Moreno and Emily Dolson},
      year={2024},
      publisher= {Association for Computing Machinery},
      address = {New York, NY, USA},
      booktitle= {Proceedings of the Genetic and Evolutionary Computation Conference Companion},
      numpages = {4},
      location = {Melbourne, VIC, Australia},
      series = {GECCO '24}
  }

citation: "Alexander Lalejini, Marcos Sanson, Jack Garbus, Matthew Andres Moreno, and Emily Dolson. 2024. Runtime phylogenetic analysis enables extreme subsampling for test-based problems. In Proceedings of the Conference on Genetic and Evolutionary Computation (GECCO '24). Association for Computing Machinery, New York, NY, USA. <https://doi.org/10.1145/3638530.3664090>"
supporting_materials: |
  - [data 1](https://osf.io/h3f52/) [via Open Science Framework ❋](https://osf.io)
  - [data 2](https://osf.io/p82cz/) [via Open Science Framework ❋](https://osf.io)
  - [source code](https://doi.org/10.5281/zenodo.10576330) [via Zenodo](https://zenodo.org/)
  - [supplemental material](https://lalejini.com/GECCO-2024-phylogeny-informed-subsampling/bookdown/book)
---
