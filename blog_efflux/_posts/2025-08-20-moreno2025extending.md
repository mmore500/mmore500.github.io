---
layout: efflux
title: "Extending a Phylogeny-based Method for Detecting Signatures of Multi-level Selection for Applications in Artificial Life"
date: 2025-08-20
permalink: "/pubs/:title"
category: conference
doi: 10.48550/arXiv.2508.14232
download: https://arxiv.org/pdf/2508.14232
view_publisher: https://arxiv.org/abs/2508.14232
authors:
  - Matthew Andres Moreno
  - Sanaz Hasanzadeh Fard
  - Emily Dolson
  - Luis Zaman
venue: The 2025 Conference on Artificial Life
projects:
  - hstrat
abstract: |
  Multilevel selection occurs when short-term individual-level reproductive interests conflict with longer-term group-level fitness effects.
  Detecting and quantifying this phenomenon is key to understanding evolution of traits ranging from multicellularity to pathogen virulence.
  Multilevel selection is particularly important in artificial life research due to its connection to major evolutionary transitions, a hallmark of open-ended evolution.
  Bonetti Franceschi & Volz (2024) proposed to detect multilevel selection dynamics by screening for mutations that appear more often in a population than expected by chance (due to individual-level fitness benefits) but are ultimately associated with negative longer-term fitness outcomes (i.e., smaller, shorter-lived descendant clades).
  Here, we use agent-based modeling with known ground truth to assess the efficacy of this approach.
  To test these methods under challenging conditions broadly comparable to the original dataset explored by Bonetti Franceschi & Volz (2024), we use an epidemiological framework to model multilevel selection in trade-offs between within-host growth rate and between-host transmissibility.
  To achieve success on our in silico data, we develop an alternate normalization procedure for identifying clade-level fitness effects.
  We find the method to be sensitive in detecting genome sites under multilevel selection with 30% effect sizes on fitness, but do not see sensitivity to smaller 10% mutation effect sizes.
  To test the robustness of this methodology, we conduct additional experiments incorporating extrinsic, time-varying environmental changes and adaptive turnover in population compositions, and find that screen performance remains generally consistent with baseline conditions.
  This work represents a promising step towards rigorous generalizable quantification of multilevel selection effects.
bibtex: |-
  @inproceedings{moreno2025extending,
    author = {Matthew Andres Moreno and Sanaz Hasanzadeh Fard and Emily Dolson and Luis Zaman},
    title = {Extending a Phylogeny-based Method for Detecting Signatures of Multi-level Selection for Applications in Artificial Life},
    booktitle = {The 2025 Conference on Artificial Life},
    collection = {ALIFE 2025},
    publisher = {MIT Press},
    year = {in press},
    doi={10.48550/arXiv.2508.14232},
    url={https://doi.org/10.48550/arXiv.2508.14232},
    month = {10},
    numpages={12},
  }
citation:  'Moreno, M. A., Hasanzadeh Fard, S., Dolson, E., & Zaman, L. (in press). Extending a Phylogeny-based Method for Detecting Signatures of Multi-level Selection for Applications in Artificial Life. In The 2024 Conference on Artificial Life. MIT Press. https://doi.org/10.48550/arXiv.2508.14232'
supporting_materials: |
  - [manuscript, notebooks, and scripts source](https://github.com/mmore500/multilevel-selection-concept/tree/v1.1.1) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [manuscript, notebooks, and scripts archive](https://doi.org/10.5281/zenodo.15549529) [via Zenodo *z*](https://zenodo.org)
  - [supplement](https://osf.io/q3fz5) [via Open Science Framework ❋](https://osf.io)
  - [data](https://osf.io/37fv8) [via Open Science Framework ❋](https://osf.io)
---
