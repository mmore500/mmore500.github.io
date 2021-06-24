---
layout: post
title: "Profiling Foundations for Scalable Digital Evolution Methods"
date: 2020-07-21
---

Digital evolution techniques compliment traditional wet-lab evolution experiments by enabling researchers to address questions that would be otherwise limited by:
* reproduction rate (which determines the number of generations that can be observed in a set amount of time),
* incomplete observations (every event in a digital system can be tracked),
* physically-impossible experimental manipulations (every event in a digital system can can be arbitrarily altered), or
* resource- and labor-intensity (digital experiments and assays can be easily automated).

The versatility and rapid generational turnover of digital systems can easily engender a notion that such systems can already operate at scales greatly exceeding biological evolution experiments.
Although digital evolution techniques can feasibly simulate populations numbering in the millions or billions, very simple agents and/or very limited agent-agent interaction.
With more complex agents controlled by genetic programs, neural networks, or the like, feasible population sizes dwindle down to thousands or hundreds of agents.

## Putting Scale in Perspective

Take Avida as an example.
This popular software system that enables experiments with evolving self-replicating computer programs.
In this system, a population of ten thousand can undergo about twenty thousand generations per day.
This means that about two hundred million replication cycles are performed in a day [[Ofria et al., 2009]](#ofria2009avida).

Each flask in the Lenski Long-Term Evolution Experiment hosts a similar number of replication cycles.
In their system, *E. coli* undergo about six doublings per day.
Effective population size is reported as 30 million [[Good et al., 2017]](#good2017dynamics).
Hence, about 180 million replication cycles elapse per day.

Likewise, in Ratcliff's work studying the evolution of multicellularity in *S. cerevisiae*, about six doublings per day occur among a population numbering on the order of a billion cells [[Ratcliff, 2012]](#ratcliff2012experimental).
So, around six billion cellular replication cycles elapse per day in this system.

Although artificial life practitioners traditionally describe instances of their simulations as "worlds," with serial processing power their scale aligns (in naive terms) more along the lines of a single flask.
Of course, such a comparison neglects the disparity between Avidians and bacteria or yeast in terms of genome information content, information content of cellular state, and both quantity and diversity of interactions with the environment and with other cells.

Recent work with SignalGP has sought to address some of these shortcomings by developing digital evolution substrates suited to more dynamic environmental and agent-agent interactions [[Lalejini and Ofria, 2018]](#lalejini2018evolving) that more effectively incorporate state information [[Lalejini et al., 2020](#lalejini2020case); [Moreno, 2020](#moreno2020evaluating)].
However, to some degree, more sophisticated and interactive evolving agents will necessarily consume more CPU time on a per-replication-cycle basis ---
further shrinking the magnitude of experiments tractable with serial processing.

## The Future is ~~Plastics~~ Parallel

Throughout the 20th century, serial processing enjoyed regular advances in computational capacity due to quickening clock cycles, burgeoning RAM caches, and increasingly clever packing together of instructions during execution.
Since, however, performance of serial processing has bumped up against apparent fundamental limits to computing's current technological incarnation [[Sutter, 2005]](#sutter2005free).
Instead, advances in 21st century computing power have arrived via multiprocessing
[[Hennessy and Patterson, 2011, p.55]](#hennessy2011computer)
and hardware acceleration (e.g., GPU, FPGA, etc.)
[[Che et al., 2008]](#che2008accelerating).

Contemporary high-performance computing clusters link multiprocessors and accelerators with fast interconnects to enable coordinated work on a single problem [[Hennessy and Patterson, 2011, p.436]](#hennessy2011computer).
High-end clusters already make [hundreds of thousands or millions](https://top500.org/) of cores available.
More loosely-affiliated banks of servers can also muster significant computational power.
For example, Sentient Technologies notably employed a distributed network of over a million CPUs to run evolutionary algorithms [[Miikkulainen et al., 2019]](#miikkulainen2019evolving).

The availability of orders of magnitude greater parallel computing resources in ten and twenty years' time seems probable, whether through incremental advances with traditional silicon-based technology or via emerging, unconventional technologies such as bio-computing [[Benenson, 2009]](#benenson2009biocomputers) and molecular electronics [[Xiang et al., 2016]](#xiang2016molecular.
Such emerging technologies could make greatly vaster collections of computing devices feasible, albeit at the potential cost of component-wise speed [[Bonnet et al., 2013](#bonnet2013amplifying); Ellenbogen and Love, 2000](#ellenbogen2000architectures)] and perhaps also component-wise reliability.

## What of Scale?

Parallel and distributed computing has long been intertwined with digital evolution [[Moreno and Ofria, 2020]](#moreno2020practical).
Practitioners typically proceed along the lines of the island model, where subpopulations evolve in parallel with intermittent exchange of individuals [[Bennett III et al., 1999]](#bennett1999building).
Similarly, in scientific contexts, absolute segregation is often enforced between parallel subpopulations to yield independent replicate datasets [[Dolson and Ofria, 2017]](#dolson2017spatial).

These techniques can enable observation of rare events and provide statistical power to answer research questions.
However, evolving subpopulations in parallel does not lend itself to large-scale study of interaction-driven phenomena such as
* multicellularity,
* sociality, and
* ecologies.

These topics are of interest in digital evolution and artificial life, particularly with respect to the issue of open-ended evolution.
While by no means certain, it seems plausible that orders-of-magnitude increases in system scale will enable qualitatively different experimental possibilities [[Moreno and Ofria, 2020]](#moreno2020practical).

So, how can we exploit parallel computing power in digital evolution systems revolving around such interaction-driven phenomena?
Addressing this question will be key both to enabling digital evolution to take full advantage of already-available contemporary computational resources and to positioning digital evolution to exploit vast computational resources that will likely become available in the not-too-distant future.

## Model Choice

In this blog series, we will investigate the scaling properties of a `std::thread`/MPI-based implementation of an asynchronous cellular automata model.

Our immediate goal is to establish a foundation for continuing work [[Moreno, 2020]](#moreno2020estimating) building a scalable implementation of the DISHTINY framework for studying digital multicellularity [[Moreno and Ofria, 2020](#moreno2020practical); [Moreno and Ofria, in prep.](#dishtinygp); [Moreno and Ofria, 2019](#moreno2019toward)].
Although the exact formulation is unimportant for the purposes of these writeups, the system might be loosely described along the lines of a grid-based cellular automata where the rule set itself is transmissible (i.e., a genetic program).

The underlying design of DISHTINY and choice of the model system profiled here is motivated by David Ackley's notion of indefinite scalability [[Ackley, 2011]](#ackley2011pursue).
In order to meaningfully function with arbitrarily large numbers of computational nodes, he argues, a system must respect:
* asynchrony,
* fault-tolerance, and
* spatial locality.

Any system operating within Ackley's framework for indefinite scalability must at least bear a passing resemblance to an asynchronous cellular automata.
So, hopefully, software tools developed and profiling results reported here might be of broader interest to researchers developing scalable artificial chemistry and artificial life simulations.

## Software Abstraction

The backbone of the prototype implementation is a "Pipe" model consisting of an `Inlet`, a `Duct`, and an `Outlet`.
Data is deposited via the `Inlet`, transmitted via the `Duct`, and received via the `Outlet`.
[Figure SOOPC](#fig-soopc) outlines how these components relate.

![pipe schematic](/resources/pipe-profile-pipe.png){:width="100%"}
[**Figure SOOPC:**](#fig-soopc){:id="fig-soopc"}
*Schematic overview of pipe components.*

API interaction occurs exclusively via the `Inlet` and the `Outlet` --- not directly with the `Duct`.
The `Duct`'s underlying transmission mechanism can be changed from intra-thread transmission to inter-thread or inter-process transmission through either the `Inlet` or the `Outlet`.

Under the hood, an `Inlet` and `Outlet` hold a `std::shared_ptr` to a `Duct`.
So, either the `Inlet` or the `Outlet` can be deleted while the `Duct` remains (as might be useful in the case of an inter-process duct).
The `Duct` contains a `std:variant` of the underlying transmission mechanisms.
This way, the underlying transmission mechanism can be changed out in-place.

Send operations into the `Inlet` are non-blocking.
However, as shown in [Figure SOOIF](#fig-sooif), in the current implementation if the `Inlet`'s buffer capacity has been reached, the send operation may drop.

![inlet schematic](/resources/pipe-profile-inlet.png){:width="100%"}
[**Figure SOOIF:**](#fig-sooif){:id="fig-sooif"}
*Schematic overview of `Inlet` function.*

Likewise, receive operations from the `Outlet` are non-blocking.
A receive operation returns the most-recently value received via the `Duct`.

![outlet schematic](/resources/pipe-profile-outlet.png){:width="100%"}
[**Figure SOOOF:**](#fig-soof){:id="fig-sooof"}
*Schematic overview of `Outlet` function.*

This software design aims to hide the complexity of wiring data heterogeneous computational elements.
As shown in [Fiure AUIFC](#fig-auifc), the exact same interface --- `Inlet`s and `Outlet`s --- performs communication within threads, between threads, or between processes.

![heterogeneouscommunication](/resources/pipe-profile-thread-proc.png){:width="100%"}
[**Figure AUIFC:**](#fig-auifc){:id="fig-auifc"}
*A uniform interface for communication within-thread, between-threads, and between-processes.*

Intra-process message passing (accomplished via MPI [[Clarke et al., 1994]](#clarke1994mpi)) allows systems built with this infrastructure to span across compute nodes.

## Model System

Using this "Pipe" API, we construct a simple one-dimensional cellular automata for use in profiling experiments.
Two states are possible.
At each update, cells adopt the state of their left neighbor --- read through an `Outlet`.
States are initialized randomly.
[Figure ASODC](#fig-asodc) summarizes.

![pipes and cells](/resources/pipe-profile-setup.png){:width="100%"}
[**Figure ASODC:**](#fig-asodc){:id="fig-asodc"}
*A simple one-dimensional cellular automata.*

## Scaling Memory & Compute

The amount of memory used per unit of computational work is crucial to the performance characteristics of software --- and varies widely between applications.
Because our goal is to characterize the general scaling properties our asynchronous communication implementation, we need to test broadly across memory-to-compute ratios.

As shown in [Figure MPVCO](#fig-mpvco), there are two levers we can pull to increase the amount of computational work in our model system.
1. We can increase the number of tiles in our one-dimensional grid.
  This increases memory use in proportion with compute.
2. We can increase the amount of computational work performed per tile update.
  This increases compute load without affecting memory use.
  (Under the hood this computational work is just increasing numbers of calls to a `thread_local` pseudorandom number generator.)

![grid size versus title work](/resources/pipe-profile-memory-proportional-compute-only.png){:width="100%"}
[**Figure MPVCO:**](#fig-mpvco){:id="fig-mpvco"}
*Memory-proportional versus compute-only scaling.*

We use these two levers to perform scaling experiments along six trajectories:
1. compute-lean,
  * memory-proportional scaling with minimal computational cost per tile update
  * increasing grid size with 1 RNG call per tile update
2. compute-moderate,
  * memory-proportional scaling with moderate computational cost per tile update
  * increasing grid size with 64 RNG calls per tile update
3. compute-intensive,
  * memory-proportional scaling with intensive computational cost per tile update
  * increasing grid size with 4096 RNG calls per tile update
4. memory-lean,
  * compute-only scaling with low memory use
  * increasing RNG calls per tile update with 1 grid tile
5. memory-moderate, and
  * compute-only scaling with moderate memory use
  * increasing RNG calls per tile update with 64 grid tiles
6. memory-intensive.
  * compute-only scaling with moderate memory use
  * increasing RNG calls per tile update with 4096 grid tiles

[Figure SSTIC](#fig-sstic) summarizes the relationship of these scaling trajectories in memory-compute space.

![scaling trajectories](/resources/pipe-profile-memory-compute.png){:width="100%"}
[**Figure SSTIC:**](#fig-sstic){:id="fig-sstic"}
*Six scaling trajectories in compute-memory space.
Each trajectory is represented as a uniquely-colored a line.
The bulb end indicates the end of the trajectory.*

## Single-Core Scaling

In order to provide a baseline characterization of our model system and our experimental scaling methods, we start by evaluating serial performance along each of our scaling trajectories.
We measure the amount of work performed in terms of the number of RNG calls dispatched.

[Figure CWRAT](#fig-cwrat) shows work rate along each scaling trajectory.

![some bar graphs](/resources/pipe-profile+Synchronous=0+title=tile-update-rate+ext=.png){:width="100%"}
[**Figure CWRAT:**](#fig-cwrat){:id="fig-cwrat"}
*Computational work rate along the scaling trajectories described in [Figure SSTIC](#fig-sstic).
Sequential bars represent increasing total work.
Along the top row, computational work and memory usage increase proportionally.
Along the bottom row, computational work increases but memory usage does not.
Error bars represent bootstrapped 95% confidence intervals.*

On the bottom row, the work rate increases as more computational work is performed per tile update.
Exactly as expected --- with more work per update a smaller and smaller fraction of time is spent communicating between grid cells and refreshing cell state.

On the top row, at low computational load (computational lean and moderate), increasing grid size decreases performance.
This could be due to memory locality worsening under a larger memory footprint --- when more memory sites are touched, cache is not as effective.

## Memory Locality

In order to further investigate the hypothesis of worsening memory locality as grid size increases at low computational load, we tried distributing work between threads on our single-core allocation.
[Figure STEOA](#fig-steoa) shows grid size before multithreading and [Figure MTEOA](#fig-mteoa) shows grid size after multithreading.

![TODO](/resources/pipe-profile-single-thread.png){:width="100%"}
[**Figure STEOA:**](#fig-steoa){:id="fig-steoa"}
*Single-threaded evaluation of an eight-tile cellular automata.*

![TODO](/resources/pipe-profile-multi-thread.png){:width="100%"}
[**Figure MTEOA:**](#fig-mteoa){:id="fig-mteoa"}
*Multi-threaded evaluation of an eight-tile cellular automata.
Each thread only evaluates two tiles.*

If memory locality was harming performance, we would expect the work rate to improve under multithreading because each thread has a smaller memory footprint.
(Although overhead of thread creation and thread switching might potentially counteract this effect.)

Here, we consider the most memory-intense scaling trajectories from [Figure SSTIC](#fig-sstic) --- where we would be most likely to observe a memory locality effect.
In [Figure NWRCL](#fig-nwrcl), work rate increases with thread count at the end of the compute-lean scaling trajectory, where memory intensity is greatest.
Likewise, in [Figure NWRMI](#fig-nwrmi), work rate increases with thread count at the beginning of the memory-intensive scaling trajectory, where memory intensity is also greatest.

![bar graphz](/resources/pipe-profile+Synchronous=0+Treatment=compute-lean+title=thread-update-rate+ext=.png){:width="100%"}
[**Figure NWRCL:**](#fig-nwrcl){:id="fig-nwrcl"}
*Net work rate by thread count at different total work loads along the compute-lean scaling trajectory.
Subplots correspond left to right to increasing total work load.
Bars within subplots correspond left to right to increasing thread count.
Error bars represent bootstrapped 95% confidence intervals.*

![bar graphz](/resources/pipe-profile+Synchronous=0+Treatment=memory-intensive+title=thread-update-rate+ext=.png){:width="100%"}
[**Figure NWRMI:**](#fig-nwrmi){:id="fig-nwrmi"}
*Net work rate by thread count at different total work loads along the memory-intensive scaling trajectory.
Subplots correspond left to right to increasing total work load.
Bars within subplots correspond left to right to increasing thread count.
Error bars represent bootstrapped 95% confidence intervals.*

These results align with the hypothesis that memory locality effects are at play.
So, we have evidence that the range of memory intensities laid out for our scaling experiments is adequately broad to be representative of more memory-bound applications.
In addition, it suggests the possibility that with an asynchronous approach we ultimately may be able to achieve a speedup by creating more threads than available cores to reduce per-thread work load and improve memory locality.

## Don't Touch That Dial!

We've reached the end of this blog post.
We've motivated and introduced the software design and evaluation methodology used, but there's still much to cover!

Upcoming material will describe,
* measuring efficiency of multithreaded and multiprocess scaling,
* measuring the distribution of message latency across threads and processes, and
* considering the effects of message size and volume.

Stay tuned!

## Cite This Post

**APA**
> Moreno, M. A. (2020, July 7). Profiling Foundations for Scalable Digital Evolution Methods. Retrieved from osf.io/tcjfy

**MLA**
> Moreno, Matthew A. “Profiling Foundations for Scalable Digital Evolution Methods.” OSF, 7 July 2020. Web.

**Chicago**
> Moreno, Matthew A. 2020. “Profiling Foundations for Scalable Digital Evolution Methods.” OSF. July 7. doi:10.17605/OSF.IO/TCJFY.

**BibTeX**
```
  @misc{Moreno_2020,
  title={Profiling Foundations for Scalable Digital Evolution Methods},
  url={osf.io/tcjfy},
  DOI={10.17605/OSF.IO/TCJFY},
  publisher={OSF},
  author={Moreno, Matthew A},
  year={2020},
  month={Jul}
}
```

## Let's Chat!

Questions?
Comments?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">nothing to see here, just a placeholder tweet 🐦</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1054071480512843776?ref_src=twsrc%5Etfw">October 21, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish: or make a comment :raising_hand_woman:

## Code & Data

We ran experiments on single-core interactive allocations on MSU ICER's `css` nodes.
Profiling results took about four hours to collect.

Data and figures are available via the [Open Science Framework](https://osf.io/) at [https://osf.io/je7ad/](https://osf.io/je7ad/) [[Foster and Deardorff, 2017]](#foster2017open).

Software used for these experiments is available [here](https://github.com/mmore500/pipe-profile/tree/je7ad).
We relied on software components from the Empirical C++ Library for Scientific Software [[Ofria et al., 2019]](#charles_ofria_2019_2575607), MPI [[Clarke et al., 1994]](#clarke1994mpi), and Matplotlib [[Hunter, 2007]](#hunter2007matplotlib).

## References

<a
  href="https://dl.acm.org/doi/10.5555/1991596.1991607"
  id="ackley2011pursue">
Ackley, D. H. and Cannon, D. C. (2011). Pursue robust indefinite scalability. In HotOS.
</a>

<a
  href="https://dl.acm.org/doi/10.5555/2934046.2934146"
  id="bennett1999building">
Bennett III, F. H., Koza, J. R., Shipman, J., and Stiffelman, O. (1999). Building a parallel computer system for $18,000 that performs a half peta-flop per day. In Proceedings of the 1st Annual Conference on Genetic and Evolutionary Computation-Volume 2, pages 1484–1490. Citeseer.
</a>

<a
  href="https://doi.org/10.1039/B902484K"
  id="benenson2009biocomputers">
Benenson, Y. (2009). Biocomputers: from test tubes to live cells. Molecular BioSystems, 5(7), 675-685.
</a>

<a
  href="https://doi.org/10.1126/science.1232758"
  id="bonnet2013amplifying">
Bonnet, J., Yin, P., Ortiz, M. E., Subsoontorn, P., & Endy, D. (2013). Amplifying genetic logic gates. Science, 340(6132), 599-603.
</a>

<a
  href="https://doi.org/10.1007/978-3-0348-8534-8_21"
  id="clarke1994mpi">
Clarke, L., Glendinning, I., and Hempel, R. (1994). The mpi message passing interface standard. In Programming environments for massively parallel distributed systems, pages 213–218. Springer.
</a>

<a
  href="http://doi.org/10.7551/ecal_a_023"
  id="dolson2017spatial">
Dolson, E. and Ofria, C. (2017). Spatial resource heterogeneity creates local hotspots of evolutionary potential. In Artificial Life Conference Proceedings 14, pages 122–129. MIT Press.
</a>

<a
  href="https://doi.org/10.1109/5.838115"
  id="ellenbogen2000architectures">
Ellenbogen, J. C., & Love, J. C. (2000). Architectures for molecular electronic computers. I. Logic structures and an adder designed from molecular electronic diodes. Proceedings of the IEEE, 88(3), 386-426.
</a>

<a
  href="http://doi.org/10.5195/jmla.2017.88"
  id="foster2017open">
Foster, E. D. and Deardorff, A. (2017). Open science framework (osf). Journal of the Medical Library Association: JMLA, 105(2):203.
</a>

<a
  href="https://doi.org/10.1038/nature24287"
  id="good2017dynamics">
Good, B. H., McDonald, M. J., Barrick, J. E., Lenski, R. E., & Desai, M. M. (2017). The dynamics of molecular evolution over 60,000 generations. Nature, 551(7678), 45–50.
</a>

<a
  href="http://doi.org/10.1109/MCSE.2007.55"
  id="hunter2007matplotlib">
Hunter, J. (2007). Matplotlib: A 2D graphics environment. Computing in Science & Engineering, 9(3), 90–95.
</a>

<a
  href="https://doi.org/10.1145/3205455.3205523"
  id="lalejini2018evolving">
Lalejini, A. and Ofria, C. (2018). Evolving event-driven programs with signalgp. In Proceedings of the Genetic and Evolutionary Computation Conference, pages 1135–1142.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/KQVMN"
  id="lalejini2020case">
Lalejini, A., Moreno, M. A., & Ofria, C. (2020, June 27). Case Study of Adaptive Gene Regulation in DISHTINY.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/RMKCV"
  id="moreno2020evaluating">
Moreno, M. A. (2020, May 1). Evaluating Function Dispatch Methods in SignalGP.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/W56BM"
  id="moreno2020estimating">
Moreno, M. A. (2020, July 8). Estimating DISHTINY Multithread Scaling Properties.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/53VGH"
  id="moreno2020practical">
Moreno, M. A., & Ofria, C. (2020, June 25). Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/G58XK"
  id="dishtinygp">
Moreno, M. A. and Ofria, C. (in prep.). Spatial constraints and kin recognition can produce open-ended major evolutionary transitions in a digital evolution system.
https://doi.org/10.17605/OSF.IO/G58XK.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00284"
  id="moreno2019toward">
Moreno, M. A. and Ofria, C. (2019). Toward open-ended fraternal transitions in individuality. Artificial life, 25(2):117–133.
</a>

<a
  href="https://doi.org/10.1007/978-1-84882-285-6_1"
  id="ofria2009avida">
Ofria C., Bryson D.M., Wilke C.O. (2009) Avida. In: Komosinski M., Adamatzky A. (eds) Artificial Life Models in Software. Springer, London
</a>

<a
  href="http://doi.org/10.5281/zenodo.2575607"
  id="charles_ofria_2019_2575607">
Ofria, C., Dolson, E., Lalejini, A., Fenton, J., Moreno, M. A., Jorgensen, S., Miller, R., Stredwick, J., Zaman, L., Schossau, J., Gillespie, L., G, N. C., and Vostinar, A. (2019). Empirical.
</a>

<a
  href="https://doi.org/10.1073/pnas.1115323109"
  id="ratcliff2012experimental">
Ratcliff, W., Denison, R., Borrello, M., & Travisano, M. (2012). Experimental evolution of multicellularity. Proceedings of the National Academy of Sciences, 109(5), 1595–1600.
</a>

<a
  href="https://doi.org/10.1021/acs.chemrev.5b00680"
  id="xiang2016molecular">
Xiang, D., Wang, X., Jia, C., Lee, T., & Guo, X. (2016). Molecular-scale electronics: from concept to function. Chemical reviews, 116(7), 4318-4440.
</a>

## Acknowledgements

This research was supported in part by NSF grants DEB-1655715 and DBI-0939454, and by Michigan State University through the computational resources provided by the Institute for Cyber-Enabled Research.
This material is based upon work supported by the National Science Foundation Graduate Research Fellowship under Grant No. DGE-1424871.
Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.
