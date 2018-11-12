---
layout: project
title: nature
description: infinite effect of a finite cause
img: /img/welcome-portfolio-lily.jpg
order: 3
---


{% for pic in site.data.nature %}
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
