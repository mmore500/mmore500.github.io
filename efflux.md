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
  <span>{{ post.title }} <br/> {{ post.venue }} </span>
  <span style="width:1em;"></span>
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </div>
  </summary>
  <div class="lollipop-detail">
  {{ post.content | markdownify }}
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
  <span style="align-self:center;"><a href="{{ post.url }}"> <i class="icon-web-page-click"></i></a></span>
  </summary>
  <div class="lollipop-detail">
  {{ post.content | markdownify }}
  </div>
  </details>
{% endfor %}
</div>
</details>

**presentation-template**. Open-source containerized LaTeX template with custom fonts. 2018. [[repository]](https://github.com/mmore500/presentation-template) [[twitter thread]](https://twitter.com/MorenoMatthewA/status/1048676082952626177)

**reinterpretive-label**. Open-source guerilla art software. 2018. [[repository]](https://github.com/mmore500/reinterpretive-label) [[twitter thread]](https://twitter.com/MorenoMatthewA/status/1011596989824405505)

**A Broadly-Conserved NERD Genetically Interacts with the Exocyst to Affect Root Growth and Cell Expansion**. Rex Cole, Valera Peremyslov, Savanah Van Why, Ibrahim Moussaoui, Ann Ketter, Renee Cool, Matthew Andres Moreno, Zuzana Vejlupkova, Valerian Dolja, and John E Fowler. Journal of Experimental Botany. May 2, 2018. [[paper]](https://academic.oup.com/jxb/advance-article/doi/10.1093/jxb/ery162/4990813?guestAccessKey=f2af1b2e-c977-4ac2-ae18-de1a3cfa6bc8)

**Understanding Fraternal Transitions in Individuality**. Matthew Andres Moreno and Charles Ofria. July, 2018. [[paper]](https://github.com/mmore500/alife-2018/releases) [[code, data, tutorials]](https://osf.io/ewvg8/) [[web demo]](https://mmore500.github.io/dishtiny/ewvg8/) [[slides]](https://github.com/mmore500/alife-2018-presentation/releases)

**Learning an Evolvable Genotype-Phenotype Mapping**. Matthew Andres Moreno, Wolfgang Banzhaf, and Charles Ofria. Proceedings of the Genetic and Evolutionary Computation Conference. July, 2018. [[paper]](https://github.com/mmore500/gecco-2018/releases) [[code, data, tutorials]](https://osf.io/n92c7/) [[blog]](https://mmore500.github.io/2018/05/23/automap.html) [[slides]](https://github.com/mmore500/gecco-2018-presentation/releases)

**templ**. Open-source Python package for organizing a Markdown notebook or journal. [[github]](https://github.com/mmore500/templ) [[blog post]](https://mmore500.github.io/2018/01/21/my-record-keeping-setup.html)

**Information Theory Through Toy Examples**. Devolab blog post. Matthew Andres Moreno. October 26, 2017. [[pdf]](/resources/october_26_2017.pdf) [[blog post]](http://devolab.org/information-theory-through-toy-examples/)

**CWLT Sunman**. Sticker Pack via MojiLaLa. Matthew Andres Moreno. August 30, 2017. [[MojiLaLa listing]]( https://mojilala.com/stickers-emojis/packages/1822f266-e798-424c-8bf6-5c386273a939) [[repository]](https://github.com/cwlt/cwlt-sunman)

**Plasticity and Evolvability in a Gene Regulatory Network Model**. Matthew Andres Moreno. Poster Session; BEACON Congress in East Lansing, Michigan. August 2, 2017. [[poster]](/resources/august_2_2017.pdf)

**Investigating the Relationship Between Plasticity and Evolvability in a
Genetic Regulatory Network Model**. Matthew Moreno. Math/CS Day; University of Puget Sound. April 29, 2017. [[presentation]](/resources/april_29_2017_presentation_capstone.pdf) [[flyer]](/resources/april_29_2017_flyer.pdf)

**MCM: Impact of Autonomous Vehicles on Seattle Traffic**. Jordan Fonseca, Jesse Jenks, and Matthew Moreno. Math/CS Day; University of Puget Sound. April 29, 2017. [[presentation]](/resources/april_29_2017_presentation_mcm.pdf) [[flyer]](/resources/april_29_2017_flyer.pdf)

**COMAP Mathematical Competition in Modeling 2017**. Matthew Moreno. Spring Experiential Learning Symposium; University of Puget Sound. April 27, 2017. [[presentation]](/resources/april_27_2017_presentation.pdf) [[flyer]](/resources/april_27_2017_flyer.pdf)

**Active Inclusivity Makes STEM Stronger**. Matthew Moreno. Washington Consortium for the Liberal Arts (WaCLA) College Essay Contest. April 24, 2017. [[essay]](/resources/april_24_2017.pdf)

**Evolvability: What Is It and How Do We Get It?**. Matthew Moreno, America Chambers, and Adam Smith. Coolidge Otis Chapman Honors Thesis. April 17, 2017. [[thesis]](http://soundideas.pugetsound.edu/honors_program_theses/22/)

**Investigating Evolvability in a Genetic Regulatory Network Model**. Matthew Moreno. Mathematics & Computer Science Seminar; University of Puget Sound. April 10, 2017. [[presentation]](/resources/april_10_2017_presentation.pdf) [[flyer]](/resources/april_10_2017_flyer.pdf)

**Modeling the Collective Behavior of Ants on Uneven Terrain**. Matthew Moreno, Jason Graham, and Simon Garnier. Phi Sigma Undergraduate Research Symposium; University of Puget Sound. April 1, 2017.  [[presentation]](/resources/april_1_2017.pdf)

**git-edit-atom**. Atom Package. March 26, 2017. [[package listing]](https://atom.io/packages/git-edit-atom)

**Evolvability: What Is It and How Do We Get It?**. Matthew Moreno. Otis C. Chapman Honors Program Thesis Presentation; University of Puget Sound. March 22, 2017. [[presentation]](/resources/march_22_2017_presentation.pdf) [[flyer]](/resources/march_22_2017_flyer.pdf)

**Silence of the Jams: The Effects of Self-Driving Cars on Traffic Patterns in the Puget Sound Region**. Jordan Fonseca, Jesse Jenks, and Matthew Moreno. CoMAP Mathematical Competition in Modeling. January 23, 2017. [[paper]](/resources/january_23_2017.pdf) [[press release]](/resources/january_23_2017_press_release.pdf) [[Seattle Times article]](/resources/january_23_2017_seattle_times.pdf)

**Modeling the Collective Behavior of Ants on Uneven Terrain**. Matthew Moreno, Jason Graham, and Simon Garnier. AMS Contributed Paper Session on Mathematical Biology; Joint Mathematics Meetings in Atlanta, Georgia. January 6, 2017.  [[presentation]](/resources/january_6_2017.pdf)

**Evolvability in Evolving Artificial Neural Networks**. Matthew Moreno. NW Honors Research Symposium; Seattle Pacific University. November 5, 2016. [[presentation]](/resources/november_5_2016.pdf)

**Modeling the Collective Behavior of Ants on Uneven Terrain**. Matthew Moreno, Jason Graham, and Simon Garnier. Undergraduate Capstone Conference; Mathematical Biosciences Institute at The Ohio State University. August 8, 2016. [[poster]](/resources/august_8_2016_poster.pdf) [[presentation]](/resources/august_8_2016_presentation.pdf)

**Relieving the Space Jam: Assessment of a Quick-Response Satellite Mission to Neutralize Debris from Orbital Fragmentation Events**. Becky Hanscam and Matthew Moreno. Math/CS Day; University of Puget Sound. April 30, 2016. [[presentation]](/resources/april_30_2016.pdf)

**What Book Has Influenced Your College Career Most, and Why?**. Matthew Moreno. Essay Competition; Puget Sound Association of Phi Beta Kappa. April 24, 2016. [[essay]](/resources/april_24_2016.pdf)

**Relieving the Space Jam: Assessment of a Quick-Response Satellite Mission to Neutralize Debris from Orbital Fragmentation Events**. Becky Hanscam, Matthew Moreno, and Caleb Spring. CoMAP Mathematical Competition in Modeling. February 1, 2016. [[paper]](/resources/february_1_2016.pdf)

**Linear Congruence Generators**. Matthew Moreno. Math 375: Probability Theory and its Applications with James Bernhard; University of Puget Sound. December 2, 2015. [[paper]](/resources/december_2_2015.pdf)

**Automated Extraction of Mouse Vocalizations from Noisy Recordings**. Matthew Moreno and Adam A Smith. Fall Poster Symposium; University of Puget Sound. September 10, 2015. [[poster]](/resources/september_10_2015.pdf)

**Mathematical Contest in Modeling: Eradicating Ebola**. Matthew Moreno. Math/CS Day; University of Puget Sound. May 2, 2015. [[presentation]](/resources/may_2_2015.pdf)

**Enantioselective Epoxide Ring Opening of Styrene Oxide with
Jacobsen’s Salen(Co) Catalyst**. Matthew Moreno and Mariah Seller. Chem 250: Organic Chemistry I with Luc Boisvert and Eric Scharrer; University of Puget Sound. December 5, 2014. [[paper]](/resources/december_5_2014.pdf)

**Screening for NERDs in Arabidopsis thaliana**. Matthew Moreno and Rex Cole. Apprenticeships in Science and Engineering Symposium; University of Portland. August 19, 2011. [[poster]](/resources/august_19_2011_poster.pdf) [[presentation]](/resources/august_19_2011_presentation.pdf)
