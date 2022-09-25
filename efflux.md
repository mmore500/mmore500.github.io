---
layout: page
title: Efflux
permalink: /efflux/
---

This page provides unrestricted downloads and supporting materials for my publications and other professional works.
My publications can also be viewed on [my google scholar profile](https://scholar.google.com/citations?user=xROn8y4AAAAJ).

{% for effluvium in site.data.effluvia %}

<details class="lollipop" {% if effluvium.open %}open{% endif %}>
<summary class="lollipop">{{ effluvium.title }}</summary>

<div class="lollipop-detail">
{% for post in site.categories.blog_efflux %}
{% if post.category == effluvium.slug %}
  <details class="lollipop">
  <summary class="lollipop">
  <div style="display:flex;flex-direction:row">
  <span style="margin-left: 0.5em; align-self:center;">{{ post.date | date: "%Y" }}</span>
  <span style="margin: 0 1em 0 0;"></span>
  <span>{{ post.title }} <br/> <i>{{ post.venue }}</i> </span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </div>
  </summary>
  <div class="lollipop-detail">
  {% include efflux_content.html page=post %}
  </div>
  </details>
  <br/>
{% endif %}
{% endfor %}
</div>

</details>

{% endfor %}

<details class="lollipop">
<summary class="lollipop">Alphabetical Listing</summary>
<div class="lollipop-detail">
{% assign sorted_posts = site.categories.blog_efflux | sort: 'title' %}
{% for post in sorted_posts  %}
  <details class="lollipop">
  <summary class="lollipop">
  <span>{{ post.title }}</span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </summary>
  <div class="lollipop-detail">
  {% include efflux_content.html page=post %}
  </div>
  </details>
{% endfor %}
</div>
</details>

<details class="lollipop">
<summary class="lollipop">Chronological Listing</summary>
<div class="lollipop-detail">
{% assign sorted_posts = site.categories.blog_efflux | sort: 'date' | reverse %}
{% for post in sorted_posts  %}
  <details class="lollipop">
  <summary class="lollipop">
  <span style="margin-left: 0.5em; align-self:center;">{{ post.date | date: "%Y" }}</span>
  <span style="margin: 0 1em 0 0;"></span>
  <span>{{ post.title }}</span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </summary>
  <div class="lollipop-detail">
  {% include efflux_content.html page=post %}
  </div>
  </details>
{% endfor %}
</div>
</details>
