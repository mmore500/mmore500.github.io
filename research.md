---
layout: page
title: Research
permalink: /research/
---

{% for post in site.categories.blog_projects %}
  <details class="lollipop">
  <summary class="lollipop">
  <div style="display:flex;flex-direction:row">
  <!-- <span style="margin-left: 0.5em; align-self:center;">{{ post.date | date: "%Y" }}</span>
  <span style="margin: 0 1em 0 0;"></span> -->
  <span style="margin-left: 0.5em;">{{ post.title }} </span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </div>
  </summary>
  <div class="lollipop-detail">
  {{ post.content | markdownify }}
  </div>
  </details>
{% endfor %}
