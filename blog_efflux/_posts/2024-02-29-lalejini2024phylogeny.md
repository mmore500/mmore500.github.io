---
layout: efflux
title: "Phylogeny-Informed Fitness Estimation for Test-Based Parent Selection"
date: 2024-02-29
permalink: "/pubs/:title"
category: chapter
download: https://arxiv.org/pdf/2306.03970.pdf
view_publisher: https://doi.org/10.1007/978-981-99-8413-8_13
authors:
  - Alexander Lalejini
  - Matthew Andres Moreno
  - Jose Guadalupe Hernandez
  - Emily Dolson 
venue: Genetic Programming Theory and Practice XX
projects:
abstract: |
  Phylogenies (ancestry trees) tell the evolutionary history of an evolving population.
  In evolutionary computing, phylogenies reveal how evolutionary algorithms steer populations through a search space by illuminating the step-by-step evolution of solutions.
  To date, phylogenetic analyses have almost exclusively been applied in post hoc analyses of evolutionary algorithms for performance tuning and research.
  Here, we apply phylogenetic information at runtime to augment parent selection procedures that use training sets to assess candidate solution quality.
  We propose phylogeny-informed fitness estimation, thinning a fraction of costly training case evaluations by substituting the fitness profiles of near relatives as a heuristic estimate.
  We evaluate phylogeny-informed fitness estimation in the context of the down-sampled lexicase and cohort lexicase selection algorithms on two diagnostic analyses and four genetic programming (GP) problems.
  Our results indicate that phylogeny-informed fitness estimation can mitigate the drawbacks of down-sampled lexicase, improving diversity maintenance and search space exploration.
  However, the extent to which phylogeny-informed fitness estimation improves problem-solving success for GP varies by problem, subsampling method, and subsampling level.
  This work serves as an initial step toward improving evolutionary algorithms by exploiting runtime phylogenetic analysis.
bibtex: |-
  @inbook{lalejini2024phylogeny,
    title    = {Phylogeny-Informed Fitness Estimation for Test-Based Parent Selection},
    author   = {Lalejini, Alexander
                and Moreno, Matthew Andres
                and Hernandez, Jose Guadalupe
                and Dolson, Emily},
    year      = 2024,
    booktitle = {Genetic Programming Theory and Practice XX},
    publisher = {Springer International Publishing},
    pages     = {241--261},
    doi       = {10.1007/978-981-99-8413-8_13},
    isbn      = {978-981-99-8413-8},
    url       = {https://doi.org/10.1007/978-981-99-8413-8_13},
    editor    = {Winkler, Stephan
                 and Trujillo, Leonardo
                 and Ofria, Charles
                 and Hu, Ting}
  }
citation: "Lalejini, A., Moreno, M.A., Hernandez, J.G., Dolson, E. (2024). Phylogeny-Informed Fitness Estimation for Test-Based Parent Selection. In: Winkler, S., Trujillo, L., Ofria, C., Hu, T. (eds) Genetic Programming Theory and Practice XX. Genetic and Evolutionary Computation. Springer, Singapore. https://doi.org/10.1007/978-981-99-8413-8_13"
supporting_materials: |
  - [data](https://osf.io/wxckn/) [via Open Science Framework ❋](https://osf.io)
  - [source code](https://doi.org/10.5281/zenodo.7938857) [via Zenodo](https://zenodo.org/)
  - [supplemental material](https://lalejini.com/GPTP-2023-phylogeny-informed-evaluation/bookdown/book/)
---
