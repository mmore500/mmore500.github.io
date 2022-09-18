---
layout: default
title: Bio, CV, etc.
permalink: /about/
---

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

<style>
details > summary {
  list-style-type: "";
  display: -webkit-flex;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: margin 150ms ease-out;
  margin-bottom: 0px;
}

details > summary:hover {
  text-decoration: underline;
}


details summary > * {
  display: inline;
}

details > summary:before {
  content: url("data:image/svg+xml; utf8, %3Csvg xmlns='http://www.w3.org/2000/svg' height='2em' width='1.25em' %3E%3Ctext x='50%25' y='50%25' font-size='1.9em' dominant-baseline='middle' text-anchor='middle'%3E⎉%3C/text%3E%3C/svg%3E");
  margin-right: 5px;
  display: -webkit-flex;
  display: flex;
  align-items: center;
  font-weight: bold;
}

details[open] > summary:before {
  content: url("data:image/svg+xml; utf8, %3Csvg xmlns='http://www.w3.org/2000/svg' height='2em' width='1.25em' %3E%3Ctext x='50%25' y='50%25' font-weight='bold' font-size='x-large' dominant-baseline='middle' text-anchor='middle'%3E◉%3C/text%3E%3C/svg%3E");
  margin-right: 5px;
  display: -webkit-flex;
  display: flex;
  align-items: center;
}

summary::-webkit-details-marker {
  list-style-type: "";
}

details[open] > summary {
  list-style-type: "";
  transition: margin 150ms ease-out;
  margin-bottom: 10px;
}

.detail {
  margin-top: -18px;
  margin-left: 0.5em;
  border-left: solid 2px;
  padding-left: 10px;
  padding-top: 12px;
  cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" style="font-size: 25px; font-weight: bold;">  <circle cx="15" cy="15" r="10" fill="white" stroke="white"/> <text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle">⎋</text></svg>'), auto;}

@keyframes details-show {
  from {
    opacity: 0;
  }
}

details[open] > *:not(summary) {
  animation: details-show 150ms ease-in-out;
}
</style>

<details onclick="if (event.target.tagName != 'A') this.removeAttribute('open');" open>
<summary>Bio<span style="width:1em;"></span> <a href="/bio"><i class="fa fa-external-link"></i></a></summary>

<div class="detail">
{% capture bio_include %}{% include bio.md %}{% endcapture %}
{{ bio_include | markdownify }}
</div>

</details>

<details onclick="if (event.target.tagName != 'A') this.removeAttribute('open');">
<summary><i>Curriculum Vitae</i><span style="width:1em;"></span> <a href="{{site.baseurl}}/resources/curriculum_vitae.pdf"><i class="fa fa-external-link"></i></a></summary>

<div class="detail">
<a href="{{site.baseurl}}/resources/curriculum_vitae.pdf">PDF <i class="fa fa-external-link"></i></a>
</div>

</details>

<details onclick="if (event.target.tagName != 'A') this.removeAttribute('open');">
<summary>Diversity, Equity, and Inclusion Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/dei-statement/"><i class="fa fa-external-link"></i></a></summary>

<div class="detail">
{% capture deis_include %}{% include professional-statements/dei.md %}{% endcapture %}
{{ deis_include | markdownify }}
</div>

</details>

<details onclick="if (event.target.tagName != 'A') this.removeAttribute('open');">
<summary>Research Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/research-statement/"><i class="fa fa-external-link"></i></a></summary>
<div class="detail">
{% capture rs_include %}{% include professional-statements/research.md %}{% endcapture %}
{{ rs_include | markdownify }}
</div>

</details>

<details onclick="if (event.target.tagName != 'A') this.removeAttribute('open');">
<summary>Teaching Statement<span style="width:1em;"></span> <a href="{{site.baseurl}}/teaching-statement/"><i class="fa fa-external-link"></i></a></summary>

<div class="detail">
{% capture ts_include %}{% include professional-statements/teaching.md %}{% endcapture %}
{{ ts_include | markdownify }}
</div>

</details>
