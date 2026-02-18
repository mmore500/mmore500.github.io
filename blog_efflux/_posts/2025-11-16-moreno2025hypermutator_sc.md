---
layout: efflux
title: "Wafer-Scale Simulation of Mutator Allele Dynamics in Large Asexual Populations"
date: 2025-11-16
permalink: "/pubs/:title"
category: abstract
download: https://sc25.supercomputing.org/proceedings/posters/poster_files/post164s2-file3.pdf
view_publisher: https://sc25.supercomputing.org/proceedings/posters/poster_pages/post164.html
authors:
  - Matthew Andres Moreno
  - Emily Dolson
  - Luis Zaman
venue: The International Conference for High Performance Computing, Networking, Storage, and Analysis (SC25)
projects:
abstract: |
  Within evolving microbial populations, genes that elevate mutation rate impose a fundamental trade-off: on one hand, increasing harmful mutations among offspring but, on the other, allowing more opportunities for rare beneficial mutations.
  Existing single-CPU agent-based simulation work suggests that increased population size should generally favor the proliferation of mutator alleles due to "hitch-hiking" effects associated with beneficial mutation discovery.
  However, in contrast to this expectation, this outcome is often not the case in large asexual populations found in nature.
  To address this knowledge gap, we leveraged the 850,000-processor Cerebras Wafer-Scale Engine (WSE) to increase simulation scale up to 1.5 billion-agent populations.
  In benchmarks, WSE provided 294x speedup over GPU and 111,091x speedup over single-core CPU execution.
  Among other results, our experiments indicate that limitation of adaptive potential (i.e., few beneficial mutations available) can produce a tertiary regime where complete mutator allele takeover becomes disfavored at very large population sizes.
bibtex: |-
  @inproceedings{moreno2025hypermutator_sc,
    author = {Matthew Andres Moreno and Emily Dolson and Luis Zaman},
    title = {Wafer-Scale Simulation of Mutator Allele Dynamics in Large Asexual Populations},
    year = {2025},
    url = {https://sc25.supercomputing.org/proceedings/posters/poster_pages/post164.html},
    booktitle = {SC25 Research Poster and ACM Student Research Competition Poster Archive},
    numpages = {2},
    location = {St. Louis, Missouri}
  }
citation: "Matthew Andres Moreno, Emily Dolson, and Luis Zaman. 2025. Wafer-Scale Simulation of Mutator Allele Dynamics in Large Asexual Populations. In SC25 Research Poster and ACM Student Research Competition Poster Archive. https://sc25.supercomputing.org/proceedings/posters/poster_pages/post164.html"
supporting_materials: |
  - [LaTeX source](https://github.com/mmore500/hypermutator-dynamics/tree/tex-sc-poster) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [poster](https://sc25.supercomputing.org/proceedings/posters/poster_files/post164s2-file2.pdf)
  - [slides](https://docs.google.com/presentation/d/12nhXl9WDB2i33-kFXYPPa4_-UtOXzcUQuBrxkmHSfSM)
---
