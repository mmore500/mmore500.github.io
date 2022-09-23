---
layout: page
title: Research
permalink: /research/
---

{% for post in site.categories.blog_projects %}
  <div class="peek_details lollipop">
  <div class="peek_summary lollipop" onclick="this.parentElement.toggleAttribute('open');">
  <div>
  <div style="display:flex;flex-direction:row;">
  <span style="margin-left: 0.5em;">{{ post.title }} </span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </div>
  </div>
  </div>
  <div class="lollipop-detail">
  <div class="peek-lollipop-mask">
  <img src="/resources/depo-consensus-problem-difficulty.png" width="100%">
  <img src="/resources/depo-consensus-problem-difficulty.png" width="100%">
  <img src="/resources/depo-consensus-problem-difficulty.png" width="100%">
  <img src="/resources/depo-consensus-problem-difficulty.png" width="100%">
  {{ post.content | markdownify }}
  </div>
  </div>
  </div>
{% endfor %}
