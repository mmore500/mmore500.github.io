---
layout: default
title: Blog
permalink: /blog/
---

<h2> <a href="here">🔗</a> here {% include icon-rss.html %} </h2>

<ul class="posts">
  {% for post in site.posts %}
  {% if post.layout == "post" %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
  {% endfor %}
</ul>

## <a href="devolab">🔗</a> [Devolab](http://devolab.msu.edu)
<ul class="posts">
  {% for post in site.data.devolab_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  <a href="http://devosoft.org/author/mmore500/">[all Devolab posts]</a>
</ul>

## <a href="elsewhere">🔗</a> elsewhere
<ul class="posts">
  {% for post in site.data.elsewhere_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a> @  <a href="{{ post.where_url }}">{{ post.where }}</a></li>
  {% endfor %}
</ul>

## <a href="recipes">🔗</a> recipes
<ul class="posts">
  {% for post in site.posts %}
  {% if post.layout == "recipe" %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
  {% endfor %}
</ul>
