---
layout: efflux
title: 'Phylotrack: C++ and Python libraries for "in silico" phylogenetic tracking'
date: 2023-08-10
permalink: "/pubs/:title"
category: preprint
download: https://github.com/openjournals/joss-papers/blob/joss.05754/joss.05754/10.21105.joss.05754.pdf
doi: "10.21105/joss.04866"
authors:
  - Emily Dolson
  - Santiago Rodriguez-Papa
  - Matthew Andres Moreno
venue: Journal of Open Source Software
projects:
  - hstrat
abstract: |
  In silico evolution instantiates the processes of heredity, variation, and differential reproductive success (the three "ingredients" for evolution by natural selection) within digital populations of computational agents.
  Consequently, these populations undergo evolution, and can be used as virtual model systems for studying evolutionary dynamics.
  This experimental paradigm --- used across biological modeling, artificial life, and evolutionary computation --- complements research done using in vitro and in vivo systems by enabling the user to conduct experiments that would be impossible in the lab or field [@dolsonDigitalEvolutionEcology2021].
  One key benefit is complete, exact observability.
  For example, it is possible to perfectly record the full set of parent-child relationships over the history of a population, yielding precise and accurate phylogenies (ancestry trees).
  This information reveals the sequences of events behind gain, loss, or maintenance of specific traits, and also facilitates making inferences about the underlying evolutionary dynamics of a given system.

  The Phylotrack project provides libraries for tracking and analyzing phylogenies in in silico evolution.
  The project is composed of 1) Phylotracklib: a header-only C++ library, developed under the umbrella of the Empirical project, and 2) Phylotrackpy: a Python wrapper around Phylotracklib, created with Pybind11.
  Both components supply a public-facing API to attach phylogenetic tracking to digital evolution systems, as well as a stand-alone interface for measuring a variety of popular phylogenetic topology metrics.
  The underlying algorithm design prioritizes efficiency, allowing Phylotrack to support large agent populations with rapid generational turnover.
  The underlying C++ implementation ensures fast, memory-efficient performance, with multiple explicit features (e.g., phylogeny pruning and abstraction, etc.) for reducing the memory footprint of phylogenetic information.
bibtex: |-
  in review
citation: in review
---
