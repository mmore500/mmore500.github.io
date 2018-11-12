---
layout: project
title: people
description: <i> Homo sapiens sapiens </i>
img: /img/people-portfolio-silhouettes.jpg
order: 1
---

{% for pic in site.data.people %}
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
