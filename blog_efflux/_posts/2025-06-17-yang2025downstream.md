---
layout: efflux
title: "Downstream: efficient cross-platform algorithms for fixed-capacity stream downsampling"
date: 2025-06-17
permalink: "/pubs/:title"
category: preprint
doi: 10.48550/arXiv.2506.12975
download: https://arxiv.org/pdf/2506.12975.pdf
view_publisher: https://doi.org/10.48550/arXiv.2506.12975
authors:
  - Connor Yang
  - Joey Wagner
  - Emily Dolson
  - Luis Zaman
  - Matthew Andres Moreno
venue: arXiv
projects:
  - hstrat
  - libraries
abstract: |
  Due to ongoing accrual over long durations, a defining characteristic of real-world data streams is the requirement for rolling, often real-time, mechanisms to coarsen or summarize stream history.
  One common data structure for this purpose is the ring buffer, which maintains a running downsample comprising most recent stream data.
  In some downsampling scenarios, however, it can instead be necessary to maintain data items spanning the entirety of elapsed stream history.
  Fortunately, approaches generalizing the ring buffer mechanism have been devised to support alternate downsample compositions, while maintaining the ring buffer's update efficiency and optimal use of memory capacity.
  The Downstream library implements algorithms supporting three such downsampling generalizations: (1) "steady," which curates data evenly spaced across the stream history; (2) "stretched," which prioritizes older data; and (3) "tilted," which prioritizes recent data.
  To enable a broad spectrum of applications ranging from embedded devices to high-performance computing nodes and AI/ML hardware accelerators, Downstream supports multiple programming languages, including C++, Rust, Python, Zig, and the Cerebras Software Language.
  For seamless interoperation, the library incorporates distribution through multiple packaging frameworks, extensive cross-implementation testing, and cross-implementation documentation.
bibtex: |-
  @misc{yang2025downstream,
        doi={10.48550/arXiv.2506.12975},
        url={https://arxiv.org/abs/2506.12975},
        title={Downstream: efficient cross-platform algorithms for fixed-capacity stream downsampling},
        author={Connor Yang and Joey Wagner and Emily Dolson and Luis Zaman and Matthew Andres Moreno},
        year={2025},
        eprint={2506.12975},
        archivePrefix={arXiv},
        primaryClass={cs.DS},
  }
citation: "Yang C., Wagner J., Dolson E., Zaman L., & Moreno M. A. (2025). Downstream: efficient cross-platform algorithms for fixed-capacity stream downsampling. arXiv preprint arXiv:2506.12975. https://doi.org/10.48550/arXiv.2506.12975"
supporting_materials: |
  - [manuscript source](https://github.com/mmore500/downstream/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software repository](https://github.com/mmore500/downstream/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [software package](https://pypi.org/project/downstream/) [via PyPI](https://pypi.org/)
  - [software package](https://crates.io/crates/downstream/) [via crates.io](https://crates.io/)
  - [notebooks](https://github.com/mmore500/downstream-benchmark/) [via GitHub <i class="icon-github-1"></i>](https://github.com/)
  - [data](https://osf.io/kjpqu/) [via Open Science Framework ❋](https://osf.io)
---
