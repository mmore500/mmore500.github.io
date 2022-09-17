---
layout: default
title: Bio
permalink: /bio/
---

{% capture bio_include %}{% include bio.md %}{% endcapture %}
{{ bio_include | markdownify }}
