---
layout: efflux
title: "Learning an Evolvable Genotype-Phenotype Mapping"
date: 2018-07-15
category: conference
download: https://github.com/mmore500/gecco-2018/releases/download/v3.1.4/sample-sigconf.pdf
view_publisher: https://doi.org/10.1145/3205455.3205597
authors:
  - Matthew Andres Moreno
  - Wolfgang Banzhaf
  - Charles Ofria
venue: The Genetic and Evolutionary Computation Conference
doi: 10.1145/3205455.3205597
abstract: |
  We present AutoMap, a pair of methods for automatic generation of evolvable genotype-phenotype mappings.
  Both use an artificial neural network autoencoder trained on phenotypes harvested from fitness peaks as the basis for a genotype-phenotype mapping.
  In the first, the decoder segment of a bottlenecked autoencoder serves as the genotype-phenotype mapping.
  In the second, a denoising autoencoder serves as the genotype-phenotype mapping.
  Automatic generation of evolvable genotype-phenotype mappings are demonstrated on the n-legged table problem, a toy problem that defines a simple rugged fitness landscape, and the Scrabble string problem, a more complicated problem that serves as a rough model for linear genetic programming.
  For both problems, the automatically generated genotype-phenotype mappings are found to enhance evolvability.
bibtex: |-
  @inproceedings{moreno2018learning,
    author = {Moreno, Matthew Andres and Banzhaf, Wolfgang and Ofria, Charles},
    title = {Learning an Evolvable Genotype-Phenotype Mapping},
    year = {2018},
    isbn = {9781450356183},
    publisher = {Association for Computing Machinery},
    address = {New York, NY, USA},
    url = {https://doi.org/10.1145/3205455.3205597},
    doi = {10.1145/3205455.3205597},
    booktitle = {Proceedings of the Genetic and Evolutionary Computation Conference},
    pages = {983–990},
    numpages = {8},
    keywords = {deep learning, indirect encodings, evolvability, genetic algorithms, adaptive representations, genotype-phenotype map},
    location = {Kyoto, Japan},
    series = {GECCO '18}
  }
citation: Matthew Andres Moreno, Wolfgang Banzhaf, and Charles Ofria. 2018. Learning an evolvable genotype-phenotype mapping. In Proceedings of the Genetic and Evolutionary Computation Conference (GECCO '18). Association for Computing Machinery, New York, NY, USA, 983–990. <https://doi.org/10.1145/3205455.3205597>
supporting_materials: |
  - [data](https://osf.io/n92c7/) [via Open Science Framework ❋](https://osf.io)
  - [how-to tutorials](https://osf.io/n92c7/wiki/) [via Open Science Framework ❋](https://osf.io)
  - [source code for *n*-legged table experiments](https://github.com/mmore500/cse-848-project) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [source code for Scrabble experiments](https://github.com/mmore500/scrabble_evo_autoencoder) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [blog post](https://mmore500.github.io/2018/05/23/automap.html)
  - [presentation](https://youtu.be/YsU8sJ9nXpg) [via YouTube <i class="icon-video"></i>](https://youtube.com)
  - [slides](https://github.com/mmore500/gecco-2018-presentation/releases/download/v1.1.0/gecco-2018-presentation.pdf)
  - [LaTeX source](https://github.com/mmore500/gecco-2018/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
---
