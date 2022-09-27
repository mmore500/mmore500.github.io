---
layout: page
title: Research
permalink: /research/
---

Agent-based evolutionary modeling enables exploration of the big-picture how and why behind incredible biological capability for adaptation, complexity, and novelty.
This field of work, known as "digital evolution," knits interdisciplinary connections between computer science and evolutionary biology to design and study digital processes and structures that capture lifelike properties.
Biologically-inspired techniques leveraging evolution as an algorithm can often produce good solutions to hard real-world problems.
They also provide a useful model system to study difficult questions in evolutionary theory.

My work focuses on understanding organisms' adaptation to the evolutionary process itself ("evolvability") and on developing methodology to simulate larger-scale digital artificial life systems, particularly with respect to high-performance computing and digital multicellularity.
I am particularly passionate about bringing research into practice by building reusable software that advances the field.

You can find more details about research projects I'm involved in below.
Selected highlights from my publications are available on my [Professional Works page](/works/).

{% for theme in site.data.project_themes %}

<div class="peek_details lollipop">
<div class="peek_summary lollipop" onclick="this.parentElement.toggleAttribute('open');">
<div>
<div style="display:flex;flex-direction:row;">
<span style="margin-left: 0.5em;">Theme: {{ theme.title }} </span>
</div>
</div>
</div>
<div class="lollipop-detail">
<div class="peek-lollipop-mask">

  {{ theme.description | markdownify }}

  {% for post in site.categories.blog_projects %}
  {% if post.theme == theme.slug %}
    <div class="peek_details lollipop">
    <div class="peek_summary lollipop" onclick="this.parentElement.toggleAttribute('open');">
    <div>
    <div style="display:flex;flex-direction:row;">
    <span style="margin-left: 0.5em;">Project: {{ post.title }} </span>
    <span style="width:1em;"></span>
    <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
    </div>
    </div>
    </div>
    <div class="lollipop-detail">
    <div class="peek-lollipop-mask">
    {% include project_content.html page=post %}
    </div>
    </div>
    </div>
  {% endif %}
  {% endfor %}

</div>
</div>
</div>

{% endfor %}
