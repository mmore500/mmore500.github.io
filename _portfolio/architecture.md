---
layout: project
title: architecture
description: the built environment
img: /img/architecture-portfolio-firehydrant.jpg
order: 2
---

{% for pic in site.data.architecture %}
<div style="text-align:center">
  <div style="display: inline-block;">
    <img src="{{ pic.href }}"  style="max-width:90vw; max-height:60vh;" alt="{{ pic.title }}">
    <br />
    <p align="left">
      {{ pic.title }}
      <br />
      {{ pic.caption }}
    </p>
  </div>
</div>
{% endfor %}
