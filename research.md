---
layout: page
title: Research
permalink: /research/
---

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
