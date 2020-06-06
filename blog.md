---
layout: default
title: Blog
permalink: /blog/
---

<h2> <a href="#here">🔗</a> here </h2>

<ul class="posts">
  {% for post in site.categories.blog_professional %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## <a href="#devolab">🔗</a> [Devolab](http://devolab.msu.edu)
<ul class="posts">
  {% for post in site.data.devolab_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
  <a href="http://devolab.org/author/mmore500/">[all Devolab posts]</a>
</ul>

## <a href="#elsewhere">🔗</a> elsewhere
<ul class="posts">
  {% for post in site.data.elsewhere_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a> @  <a href="{{ post.where_url }}">{{ post.where }}</a></li>
  {% endfor %}
</ul>

## <a href="#mentees_collaborators">🔗</a> mentees & collaborators
<ul class="posts">
  {% for post in site.data.mentees_collaborators_posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a> by <a href="{{ post.who_url }}">{{ post.who }}</a> @ <a href="{{ post.where_url }}">{{ post.where }}</a></li>
  {% endfor %}
</ul>

## <a href="#personal">🔗</a> personal
<ul class="posts">
  {% for post in site.categories.blog_personal %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## <a href="#recipes">🔗</a> recipes
<ul class="posts">
  {% for post in site.categories.blog_recipes %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
