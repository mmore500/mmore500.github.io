---
layout: post
title:  "Case Study of Adaptive Gene Regulation in DISHTINY"
date:   2020-06-26
no_toc: true
---

## Introduction

The DISHTINY artificial life system [[Moreno and Ofria, 2019]](#moreno2019toward) is designed to study fraternal transitions in individuality, evolutionary events where independently replicating entities unify into a higher-level individual.
Multicellular organisms and eusocial insect colonies, which survive and propagate through the cooperation of lower-level kin, are typical exemplars of fraternal transitions [[Smith and Szathmary, 1997]](#smith_major_1997).

## Methods

DISHTINY tracks autonomous self-replicating digital cells with heritable behavioral strategies situated on a two-dimensional toroidal grid.
Cells can form spatial kin groups to cooperatively collect resources.
The morphology of these groups is determined by where offspring are placed and whether they remain part of the parent's group or are expelled to bud a new group.
These conditions yield evolved strategies where individual cells perform actions contrary to their immediate interests (\textit{e.g.}, suppressing reproduction, giving away resources, or even self-destructing) to benefit their kin group [[Moreno and Ofria, in prep]](#moreno_dishtinygp_inprep).

In current work with DISHTINY, SignalGP programs manage cellular behavior.
Within each cell, four interconnected hardware instances independently execute a single genetic program; each instance controls cell behavior with respect to a cardinal direction.
Sensor instructions and event-driven cues allow cells to react to local information.
Likewise, special instructions enable local actions (such as reproduction, resource sharing, and messaging).
SignalGP function regulation operates as in the repeated- and changing-signal tasks, except function regulation decays to a neutral baseline unless explicitly renewed.

Evolved DISHTINY populations analyzed here were drawn from ongoing work investigating cell-cell interconnects.
We analyze 64 replicate populations each evolved independently for 200 compute-hours under identical evolutionary conditions (mean 62912, S.D. 32840 cellular generations elapsed).

<!-- % Output saved to title=mastergenerations+_data_hathash_hash=bfb767476178d32a+_script_fullcat_hash=5e6b7a64514cbb09+_source_hash=aa98eba-clean+ext=.csv
% level 0
% Generations Elapsed mean 62912.675239398755
% Generations Elapsed std 32840.164094750195
% Generations Elapsed min 18512.706334458795
% Generations Elapsed max 117682.51523342053
% level 1
% Generations Elapsed mean 43764.47479221449
% Generations Elapsed std 22848.796707961814
% Generations Elapsed min 8392.893406159901
% Generations Elapsed max 71774.90111067913
% level 2
% Generations Elapsed mean 7634.921648085374
% Generations Elapsed std 3539.0957581514363
% Generations Elapsed min 2697.1663356846066
% Generations Elapsed max 13602.845348683946 -->

(See [[Moreno and Ofria, 2020b]](#Moreno_Ofria_2020b) for details.)

## Implementation

We implemented our experimental system using the Empirical library for scientific software development in C++, available at [`https://github.com/devosoft/Empirical`](https://github.com/devosoft/Empirical) [[Ofria et al., 2019]](#charles_ofria_2019_2575607).
We used OpenMP to parallelize our main evolutionary replicates, distributing work over two threads.
The code used to perform and analyze our experiments, our figures, data from our experiments, and a live in-browser demo of our system is available via the Open Science Framework at [`https://osf.io/kqvmn/`](https://osf.io/kqvmn/) [[Foster and Deardorff, 2017]](#foster2017open).

## Results

We used knockout experiments to measure the fraction of replicates that adaptively employ genetic regulation.
We harvested a representative genotype from each of the 64 evolved DISHTINY populations.
For each independently-evolved population, we performed 16 competition experiments between the representative genotype and a corresponding strain where gene regulation was knocked out.
We seeded these runs half-and-half with wild-type and derived knockout genotypes.
After one hour of compute time, we assessed the relative abundance of cells descended from wild-type and knockout ancestors.
Within the one-hour window, a mean of 91 (S.D. 38) cellular generations elapsed and 17\% of competition runs had coalesced to only the wild type or the knockout strain.

<!-- % Output saved to title=mastergenerations+_data_hathash_hash=d7e5733d345116b5+_script_fullcat_hash=5e6b7a64514cbb09+_source_hash=e23c716-clean+ext=.csv
% level 0
% Generations Elapsed mean 90.74286163476415
% Generations Elapsed std 38.36954058701016
% Generations Elapsed min 18.114492929551094
% Generations Elapsed max 181.66094266246537
% level 1
% Generations Elapsed mean 62.64397708025472
% Generations Elapsed std 31.212924615862303
% Generations Elapsed min 18.114300356358296
% Generations Elapsed max 164.4504889317493
% level 2
% Generations Elapsed mean 10.227281633001045
% Generations Elapsed std 4.330477728861442
% Generations Elapsed min 1.6648833273095958
% Generations Elapsed max 20.90711371898312 -->

For 10 out of 64 populations, all 16 competition runs exhibited greater abundance of cells descended from the wild-type strain than the knockout strain.
Gene regulation contributed significantly to fitness in these runs
(Fisher's exact test with Bonferroni correction, each $p < 0.001$).
Among these 10 independently-evolved genotypes, gene regulation plays an adaptive role.
However, it is possible that in these cases, gene regulation represents non-plastic contingency rather than contributing to meaningful functionality.

To address this question, we compared the fitnesses of strains that relied on regulation to strains that did not.
We measured strain fitness by competing it against a randomly sampled panel of 20 evolved genotypes.
We did not find evidence that strains that used gene regulation outperformed strains that did not.

![](/resources/regulation-dishtiny-regulation-pca.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}

[**Figure PVOGR:**](#fig-pvogr){:id="fig-pvogr"}
_PCA visualization of gene regulation in case-study evolved genotype._

Shifting our approach, we selected a strain from among the 10 to evaluate further as a case study to test for a functional role of gene regulation ([Figure PVOGR](#fig-pvogr); live in-browser viewer at [`mmore500.com/hopto/5`](https://mmore500.com/hopto/5)).
We confirmed that in this strain gene regulation plays a bona fide functional role facilitating coordination among same-cell SignalGP instances.
[Figure FCOGR](#fig-fcogr)(a) summarizes the functional context of gene regulation in this strain.
We inferred relationships between components in this diagram by monitoring hardware execution in a monoculture population with mutation disabled.
Component-by-component knockout experiments confirmed the adaptive significance of each element of the interaction diagram.
We hypothesize that gene regulation mediates intracell mutual exclusion (see [Figure FCOGR](#fig-fcogr)(b)).

![](/resources/regulation-dishtiny-logic-diagram.png){:style="width: 100%;"}
_(a) Regulation governs cell division based on environmental state and intracellular state.
In baseline conditions, stimulus 1 would activate module A, expressing cell division instructions.
However, when module B represses module A, this stimulus instead activates module C --- leaving module A unexpressed.
This mechanism conditions expression of module A on stimulus 1, but neither of stimulus 2 or 3.
Module A also contains instructions to broadcast an intracellular message that activates module B in a cell's other independently-executing SignalGP instances._

![](/resources/regulation-dishtiny-cell-diagram.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}
_(b) Intracellular broadcast delivers a message to each of a cell's other SignalGP instances, activating their module 14 and subsequently repressing their module 2._

[**Figure FCOGR:**](#fig-fcogr){:id="fig-fcogr"}
_Functional context of gene regulation in a case-study evolved genotype._

[Figure SPOGR](#fig-spogr) shows the spatial expression and regulation patterns of modules A, B, and C.
Indeed, in some instances, we can observe expression of module A in a single hardware instance within cells next to two different-group neighbors.
However, we can also observe the opposite in other instances, presumably due to interfering cellular mechanisms and virtual hardware limitations
(e.g., inbox capacity, thread capacity, concurrency effects, latency effects, conditional message blocking, and thread requisition).

![](/resources/regulation-dishtiny-f0-1000.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}
_(a) Module 0 expression snapshot._

![](/resources/regulation-dishtiny-f2-1000.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}
_(b) Module 2 expression snapshot._

![](/resources/regulation-dishtiny-f14-1000.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}
_(c) Module 14 expression snapshot._

![](/resources/regulation-dishtiny-r2-1000.png){:style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;"}
_(d) Module 2 regulation snapshot._

[**Figure SPOGR:**](#fig-fcogr){:id="fig-fcogr"}
_Spatial patterns of gene regulation and module expression.
Square tiles represent individual cells.
Black borders divide cells belonging to different organisms.
Cells are divided into four triangle slices, each corresponding to a independently-executing SignalGP instance.
In module expression snapshots, white denotes no expression, green denotes a module running on a single hardware core, blue on two, purple on three, red on four, and silver on five.
In module regulation shapshots, white denotes baseline state and blue denotes repression._


## Let's Chat

I would love to hear your thoughts on artificial life models of gene regulation and studying major transitions in evolution!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">nothing to see here, just a placeholder tweet 🐦</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1054071480512843776?ref_src=twsrc%5Etfw">October 21, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish: or make a comment :raising_hand_woman:

## Cite This Post

**APA**
> Lalejini, A., Moreno, M. A., & Ofria, C. (2020, June 27). Case Study of Adaptive Gene Regulation in DISHTINY. https://doi.org/10.17605/OSF.IO/KQVMN

**MLA**
> Lalejini, Alexander, Matthew A Moreno, and Charles Ofria. “Case Study of Adaptive Gene Regulation in DISHTINY.” OSF, 27 June 2020. Web.

**Chicago**
> Lalejini, Alexander, Matthew A Moreno, and Charles Ofria. 2020. “Case Study of Adaptive Gene Regulation in DISHTINY.” OSF. June 27. doi:10.17605/OSF.IO/KQVMN.

**BibTeX**
```
@misc{Lalejini_Moreno_Ofria_2020,
  title={Case Study of Adaptive Gene Regulation in DISHTINY},
  url={osf.io/kqvmn},
  DOI={10.17605/OSF.IO/KQVMN},
  publisher={OSF},
  author={Lalejini, Alexander and Moreno, Matthew A and Ofria, Charles},
  year={2020},
  month={Jun}
}
```

## References

<a
  href="http://doi.org/10.5195/jmla.2017.88"
  id="foster2017open">
Foster, E. D. and Deardorff, A. (2017). Open science framework (osf). Journal of the Medical Library Association: JMLA, 105(2):203.
</a>

<a
  href="https://doi.org/10.1145/3205455.3205523"
  id="lalejini2018evolving">
Lalejini, A. and Ofria, C. (2018). Evolving event-driven programs with signalgp. In Proceedings of the Genetic and Evolutionary Computation Conference, pages 1135–1142.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00284"
  id="moreno2019toward">
Moreno, M. A. and Ofria, C. (2019). Toward open-ended fraternal transitions in individuality. Artificial life, 25(2):117–133.
</a>

<a
  href="http://doi.org/10.17605/OSF.IO/KQVMN"
  id="Moreno_Ofria_2020a">
Moreno, M. A. and Ofria, C. (2020a). Case Study of Adaptive Gene Regulation in DISHTINY. DOI: 10.17605/OSF.IO/KQVMN; URL: https://osf.io/kqvmn.
</a>

<!-- <a
  href="http://doi.org/10.17605/OSF.IO/53VGH"
  id="Moreno_Ofria_2020b">
Moreno, M. A. and Ofria, C. (2020ab). Practical steps toward indefinite scalability: In pursuit of robust computational substrates for open-ended evolution. DOI: 10.17605/OSF.IO/53VGH; URL: https://osf.io/53vgh.
</a> -->

<a
  href="https://doi.org/10.17605/OSF.IO/G58XK"
  id="dishtinygp">
Moreno, M. A. and Ofria, C. (in prep.). Spatial constraints and kin recognition can produce open-ended major evolutionary transitions in a digital evolution system.
https://doi.org/10.17605/OSF.IO/G58XK.
</a>

<a
  href="http://doi.org/10.5281/zenodo.2575607"
  id="charles_ofria_2019_2575607">
Ofria, C., Dolson, E., Lalejini, A., Fenton, J., Moreno, M. A., Jorgensen, S., Miller, R., Stredwick, J., Zaman, L., Schossau, J., Gillespie, L., G, N. C., and Vostinar, A. (2019). Empirical.
</a>

<a
  href="http://www.worldcat.org/oclc/1004817525"
  id="smith_major_1997">
Smith, J. M. and Szathmary, E. (1997). The major transitions in evolution. Oxford University Press.
</a>

## Acknowledgements

This research was supported in part by NSF grants DEB-1655715 and DBI-0939454, and by Michigan State University through the computational resources provided by the Institute for Cyber-Enabled Research.
This material is based upon work supported by the National Science Foundation Graduate Research Fellowship under Grant No. DGE-1424871.
Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.
