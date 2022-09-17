---
layout: default
title: Bio, CV, etc.
permalink: /about/
---

<details>
<summary>Bio</summary>

{% capture bio_include %}{% include bio.md %}{% endcapture %}
{{ bio_include | markdownify }}

</details>

<details>
<summary><i>Curriculum Vitae</i></summary>



</details>

<details>
<summary>Diversity, Equity, and Inclusion Statement</summary>

{% capture deis_include %}{% include professional-statements/dei.md %}{% endcapture %}
{{ deis_include | markdownify }}

</details>

<details>
<summary>Research Statement</summary>

{% capture rs_include %}{% include professional-statements/research.md %}{% endcapture %}
{{ rs_include | markdownify }}

</details>

<details>
<summary>Teaching Statement</summary>

{% capture ts_include %}{% include professional-statements/teaching.md %}{% endcapture %}
{{ ts_include | markdownify }}

</details>
