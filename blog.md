---
layout: default
title: Blog
permalink: /blog/
---

<h2> here {% include icon-rss.html %} </h2>

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## [Devolab](http://devolab.msu.edu)
<ul class="posts">
  {% for post in site.data.devolab_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  <a href="http://devosoft.org/author/mmore500/">[all Devolab posts]</a>
</ul>

## elsewhere
<ul class="posts">
  {% for post in site.data.elsewhere_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a> @  <a href="{{ post.where_href }}">{{ post.where }}</a></li>
  {% endfor %}
</ul>
