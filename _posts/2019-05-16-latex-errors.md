---
layout: post
title:  "Common LaTeX Errors"
date:   2019-05-16
no_toc: true
---

## The List

The following snippets show a LaTeX error followed by the proper coding of the author's intent.

Improper use of quotation marks.

~~~
The circus was the "greatest."

The circus was the ``greatest.''
~~~

Accidentally dropping multi-character superscripts to the baseline.

~~~
I add terms $a^9$ and $a^10$ to get $a^11$.

I add terms $a^{9}$ and $a^{10}$ to get $a^{11}$.
~~~

Same thing, but with respect to subscripts.

~~~
I add terms $a_9$ and $a_10$ to get $a_11$.

I add terms $a_{9}$ and $a_{10}$ to get $a_{11}$.
~~~

Using improperly typeset ellipses.

~~~
We multiply $x \times y \times ... \times z$.

We multiply $x \times y \times \cdots \times z$.
~~~

Using less-than/greater-than sign instead of angle brackets.

~~~
The vector we are working with is $<x,y>$.

The vector we are working with is $\langle x, y \rangle$.
~~~

Using math mode instead of italicization.

~~~
I $really$ mean it.

I \textit{really} mean it.
~~~

Not enforcing spaces after LaTeX commands.

~~~
\LaTeX is fun.

\LaTeX{} is fun.
~~~

## Open Pedagogical Research Question

[LaTeX](https://www.latex-project.org/) is a ubiquitous document preparation system in the sciences, in particular mathematics.
Unlike document preparations systems like Microsoft Word and Google Docs, LaTeX is not "what you see is what you get."
Instead of working in a live preview of a document, you write LaTeX code, compile the document (e.g., it renders to a PDF), and then view the document.

In part based on my own experience, I suspect that LaTeX skills are not typically learned in a formal setting.
My own introduction to LaTeX in Linear Algebra consisted basically of a template document to extend and direction to an online compilation service called [Overleaf](https://www.overleaf.com/).
I grew my LaTeX knowledge on an ad-hoc need-to-know basis, mostly via [Google](https://google.com) and [Stack Overflow](https://tex.stackexchange.com/).
Occasionally, I received LaTeX-specific feedback on my homework submissions.
I remember, in particular, once being told --- good-naturedly --- what I was writing Tex "like an emeritus professor."

I suspect that inside the mathematics/science community, TeX proficiency is often taken as a proxy for the competency/authority of a mathematician/scientist.
This phenomena might involve both conscious and subconscious elements.
Such an attitude might have implications on how --- and to who --- credibility/authority/career advancement is distributed in mathematics and the sciences.

Back when I worked at the [CWLT](https://pugetsound.edu/cwlt), I sketched out a pedagogical research project centered around a question motivated by these observations, "Do LaTeX errors impact evaluator's judgment of a student's conceptual mastery?"

I never got around to pursuing this question, but if it piques someone else's interest an experiment could be run as follows:

1. Collect several prompts for short proofs from mathematics courses (perhaps at both introductory and advanced levels).
2. Collect or synthesize proofs responding to these prompts.
3. Create alternate versions of these proofs that are identical except for the addition of typesetting errors (like those listed above).
4. Distribute these proofs to math professors and ask that they evaluate conceptual mastery.
  For each proof, a professor should probably only receive one of the alternate typesettings.
  The addition of other dummy questions to disguise the intent of the study might also be considered.
  Some consideration of study design (i.e., re: planned statistical analysis) would be required at this step.
5. Collect the data 'n do the stats to test for significant differences in evaluated mastery between error-containing and error-free proofs.

I chose the examples above because they are purely technical and specific to LaTeX --- they do not involve the potential complicating factor of style.

## Let's Chat

Comments? Questions?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">threw up a blog with some common LaTeX errors and an open pedagogical research question<a href="https://t.co/R32MNFdAnV">https://t.co/R32MNFdAnV</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1129073716330147841?ref_src=twsrc%5Etfw">May 16, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
