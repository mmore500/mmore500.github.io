---
layout: page
title: Efflux
permalink: /efflux/
---

This page provides unrestricted downloads and supporting materials for my publications and other professional works.
My publications can also be viewed on [my google scholar profile](https://scholar.google.com/citations?user=xROn8y4AAAAJ).

{% for effluvium in site.data.effluvia %}

<details class="lollipop">
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

**Information Theory Through Toy Examples**. Devolab blog post. Matthew Andres Moreno. October 26, 2017. [[pdf]](/resources/october_26_2017.pdf) [[blog post]](http://devolab.org/information-theory-through-toy-examples/)

**Plasticity and Evolvability in a Gene Regulatory Network Model**. Matthew Andres Moreno. Poster Session; BEACON Congress in East Lansing, Michigan. August 2, 2017. [[poster]](/resources/august_2_2017.pdf)

**Investigating the Relationship Between Plasticity and Evolvability in a
Genetic Regulatory Network Model**. Matthew Moreno. Math/CS Day; University of Puget Sound. April 29, 2017. [[presentation]](/resources/april_29_2017_presentation_capstone.pdf) [[flyer]](/resources/april_29_2017_flyer.pdf)

**MCM: Impact of Autonomous Vehicles on Seattle Traffic**. Jordan Fonseca, Jesse Jenks, and Matthew Moreno. Math/CS Day; University of Puget Sound. April 29, 2017. [[presentation]](/resources/april_29_2017_presentation_mcm.pdf) [[flyer]](/resources/april_29_2017_flyer.pdf)

**Investigating Evolvability in a Genetic Regulatory Network Model**. Matthew Moreno. Mathematics & Computer Science Seminar; University of Puget Sound. April 10, 2017. [[presentation]](/resources/april_10_2017_presentation.pdf) [[flyer]](/resources/april_10_2017_flyer.pdf)

**Silence of the Jams: The Effects of Self-Driving Cars on Traffic Patterns in the Puget Sound Region**. Jordan Fonseca, Jesse Jenks, and Matthew Moreno. CoMAP Mathematical Competition in Modeling. January 23, 2017. [[paper]](/resources/january_23_2017.pdf) [[press release]](/resources/january_23_2017_press_release.pdf) [[Seattle Times article]](/resources/january_23_2017_seattle_times.pdf)
