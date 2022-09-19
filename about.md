---
layout: default
title: About
permalink: /about/
---

<details class="lollipop" open>
<summary class="lollipop">Bio<span style="width:1em;"></span> <a href="/bio"><i class="icon-web-page-click"></i></a></summary>

<div class="lollipop-detail exit-cursor" onclick="if (event.target.tagName != 'A') this.parentElement.removeAttribute('open');">

{% capture bio_include %}{% include bio.md %}{% endcapture %}
{{ bio_include | markdownify }}
</div>

</details>

<details class="lollipop">
<summary class="lollipop"><i>Curriculum Vitae</i><span style="width:1em;"></span> <a href="{{site.baseurl}}/resources/curriculum_vitae.pdf"><i class="icon-web-page-click"></i></a></summary>

<div class="lollipop-detail exit-cursor" onclick="if (event.target.tagName != 'A') this.parentElement.removeAttribute('open');">
<a href="{{site.baseurl}}/resources/curriculum_vitae.pdf">PDF <i class="icon-web-page-click"></i></a>
</div>

</details>

<details class="lollipop">
<summary class="lollipop">Diversity, Equity, and Inclusion Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/dei-statement/"><i class="icon-web-page-click"></i></a></summary>

<div class="lollipop-detail exit-cursor" onclick="if (event.target.tagName != 'A') this.parentElement.removeAttribute('open');">

{% capture deis_include %}{% include professional-statements/dei.md %}{% endcapture %}
{{ deis_include | markdownify }}
</div>

</details>

<details class="lollipop">
<summary class="lollipop">Research Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/research-statement/"><i class="icon-web-page-click"></i></a></summary>
<div class="lollipop-detail exit-cursor" onclick="if (event.target.tagName != 'A') this.parentElement.removeAttribute('open');">

{% capture rs_include %}{% include professional-statements/research.md %}{% endcapture %}
{{ rs_include | markdownify }}
</div>

</details>

<details class="lollipop">
<summary class="lollipop">Teaching Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/teaching-statement/"><i class="icon-web-page-click"></i></a></summary>

<div class="lollipop-detail exit-cursor" onclick="if (event.target.tagName != 'A') this.parentElement.removeAttribute('open');">

{% capture ts_include %}{% include professional-statements/teaching.md %}{% endcapture %}
{{ ts_include | markdownify }}
</div>

</details>
