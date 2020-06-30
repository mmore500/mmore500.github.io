---
layout: post
title:  "Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution"
date:   2020-06-23
---

## Abstract

Studying how artificial evolutionary systems can continually produce novel artifacts of increasing complexity has proven to be a rich vein for practical, scientific, philosophical, and artistic innovations.
Unfortunately, existing computational artificial life systems appear constrained by practical limitations on simulation scale.
The concept of indefinite scalability describes constraints on open-ended systems necessary to incorporate theoretically unbounded computational resources.
Here, we argue that along the path to indefinite scalability, we must consider practical scalability: how can we design open-ended evolutionary systems that make effective use of existing, commercially-available distributed-computing hardware?
We highlight log-time hardware interconnects as a potentially fruitful tool for practical scalability and describe how digital evolution systems might be constructed to exploit physical log-time interconnects.
We extend the DISHTINY digital multicellularity framework to allow cells to establish long-distance cell-cell interconnects that, in implementation, could take advantage of log-time physical interconnects.
We examine two case studies of evolved strains, demonstrating how evolved cells adaptively exploit these interconnects.

## Introduction

The challenge, and promise, of open-ended evolution has animated decades of inquiry and discussion within the artificial life community [[Packard et al., 2019]](#packard2019overview).
The difficulty of devising models that produce characteristic outcomes of open-ended evolution suggests profound philosophical or scientific blind spots in our understanding of the natural processes that gave rise to contemporary organisms and ecosystems.
Already, pursuit of open-ended evolution has yielded paradigm-shifting insights.
For example, novelty search demonstrated how processes promoting non-adaptive diversification can ultimately yield adaptive outcomes that were previously unattainable [[Lehman and Stanley, 2011]](#lehman2011abandoning).
Such work lends insight to fundamental questions in evolutionary biology, such as the relevance --- or irrelevance -- of natural selection with respect to increases in complexity
[[Lehman, 2012](#lehman2012evolution);
[Lynch, 2007](#lynch2007frailty)]
and the origins of evolvability
[[Lehman and Stanley, 2013](#lehman2013evolvability);
[Kirschner and Gerhart, 1998](#kirschner1998evolvability)].
Evolutionary algorithms devised in support of open-ended evolution models also promise to deliver tangible broader impacts on society.
Possibilities include the generative design of engineering solutions, consumer products, art, video games, and AI systems
[[Nguyen et al., 2015](#nguyen2015innovation); [Stanley et al., 2017](#stanley2017open)].

Preceding decades have witnessed advances toward defining --- quantitatively and philosophically --- the concept of open-ended evolution
[[Lehman and Stanley, 2012](#lehman2012beyond); [Dolson et al., 2019](#dolson2019modes);
[Bedau et al., 1998](#bedau1998classification)]
as well as investigating causal phenomena that promote open-ended dynamics such as ecological dynamics, selection, and evolvability
[[Dolson, 2019](#dolson2019constructive);
[Soros and Stanley, 2014](#soros2014identifying);
[Huizinga et al., 2018](#huizinga2018emergence)].
Together, methodological and theoretical advances have begun to yield evidence that the generative potential of artificial life systems is --- at least in part --- meaningfully constrained by available compute resources [[Channon, 2019]](#channon2019maximum).

### Advances in Modern Compute Resources Rely on Distribution and Parallelism

Since the turn of the century, advances in the clock speed of traditional serial processors have trailed off [[Sutter, 2005]](#sutter2005free).
Existing technologies have begun to encounter fundamental constraints including power use and thermal dissipation [[Markov, 2014]](#markov2014limits).
Instead, hardware innovation began to revolve around multiprocessing
[[Hennessy and Patterson, 2011, p.55]](#hennessy2011computer)
and hardware acceleration (e.g., GPU, FPGA, etc.)
[[Che et al., 2008]](#che2008accelerating).
For scientific and engineering applications, individual multiprocessors and accelerators are joined together with fast interconnects to yield so-called high-performance computing clusters s [[Hennessy and Patterson, 2011, p.436]](#hennessy2011computer).
Until fundamental changes to computing technology transpire, scaling up artificial life compute power will require taking advantage of these existing parallel and distributed systems.

### Distributed Hardware in Digital Evolution

Digital evolution practitioners have a rich history of leveraging distributed hardware.
It is common practice to distribute multiple self-isolated instantiations of evolutionary runs over multiple hardware units.
In scientific contexts, this practice yields replicate datasets that provide statistical power to answer research questions [[Dolson and Ofria,
2017]](#dolson2017spatial).
In applied contexts, this practice yields many converged populations that can be scavenged for the best solutions overall [[Hornby et al., 2006]](#hornby2006automated).

Another established practice is to use "island models" where individuals are transplanted between populations that are otherwise independently evolving across distributed hardware.
Koza and collaborators' genetic programming work with a 1,000-cpu Beowulf cluster typifies this approach [[Bennett III et al., 1999]](#bennett1999building).

In recent years, Sentient Technologies spearheaded digital evolution projects on an unprecedented computational scale, comprising over a million CPUs and capable of a peak performance of 9 petaflops [[Miikkulainen et al., 2019]](#miikkulainen2019evolving).
According to its proponents, the scale and scalability of this DarkCycle system was a key aspect of its conceptualization [[Gilbert, 2015]](#gilbert_2015).
Much of the assembled infrastructure was pieced together from heterogeneous providers and employed on a time-available basis [[Blondeau et al., 2012]](#blondeau2012distributed).
Unlike island model where selection events are performed independently on each CPU, this scheme transferred evaluation criteria between computational instances (in addition to individual genomes) [[Hodjat and Shahrzad, 2013]](#hodjat2013distributed).

Sentient Technologies also accelerated the deep learning training process by using many massively-parallel hardware accelerators (e.g., 100 GPUs) to evaluate the performance of candidate neural network architectures on image classification, language modeling, and image captioning problems [[Miikkulainen et al., 2019]](#miikkulainen2019evolving).
Analogous work parallelizing the evaluation of an evolutionary individual over multiple test cases in the context of genetic programming has used GPU hardware and vectorized CPU operations
[[Harding and Banzhaf, 2007b](#harding2007fast2);
[Langdon and Banzhaf, 2019](#langdon2019continuous)].

Existing applications of concurrent approaches to digital evolution distribute populations or individuals across hardware to process them with minimal interaction.
Task independence facilitates this simple, efficient implementation strategy, but precludes application on elements that are not independent.
Parallelizing evaluation of a single individual often emphasizes data-parallelism over independent test cases, which are subsequently consolidated into a single fitness profile.
With respect to model parallelism, Harding has notably applied GPU acceleration to cellular automata models of artificial development systems, which involve intensive interaction between spatially-distributed instantiation of a genetic program [[Harding and Banzhaf, 2007a]](#harding2007fast).
However, in systems where evolutionary individuals themselves are parallelized they are typically completely isolated from each other.

We argue that, in a manner explicitly accommodating capabilities and limitations of available hardware, open-ended evolution should prioritize dynamic interactions between simulation elements situated across physically distributed hardware components.

### Leveraging Distributed Hardware for Open-Ended Evolution

Unlike most existing applications of distributed computing in digital evolution, open-ended evolution researchers should prioritize dynamic interactions among distributed simulation elements.
Parallel and distributed computing enables larger populations and metapopulations.
However, ecologies, co-evolutionary dynamics, and social behavior all necessitate dynamic interactions among individuals.

Distributed computing should also enable more computationally intensive or complex individuals.
Developmental processes and emergent functionality necessitate dynamic interactions among components of an evolving individual.
Even at a scale where individuals remain computationally tractable on a single hardware component, modeling them as a collection of discrete components configured through generative development (i.e., with indirect genetic representation) can promote scalable properties
[[Lipson, 2007]](#lipson2007principles)
such as modularity, regularity, and hierarchy
[[Hornby, 2005](#hornby2005measuring);
[Clune et al., 2011](#clune2011performance)].
Developmental processes may also promote canalization
[[Stanley and Miikkulainen, 2003]](#stanley2003taxonomy),
for example through exploratory processes and compensatory adjustments
[[Gerhart and Kirschner, 2007]](#gerhart2007theory).
To reach this goal, David Ackley has envisioned an ambitious design for modular distributed hardware at a theoretically unlimited scale
[[Ackley and Cannon, 2011]](#ackley2011pursue)
and demonstrated an algorithmic substrate for emergent agents that can take advantage of it
[[Ackley, 2018]](#ackley2018digital).

### A Path of Expanding Computational Scale

While by no means certain, the idea that orders-of-magnitude increases in compute power will open up qualitatively different possibilities with respect to open-ended evolution is well founded.
Spectacular advances achieved with artificial neural networks over the last decade illuminate a possible path toward this outcome.
As with digital evolution, artificial neural networks (ANNs) were traditionally understood as a versatile, but auxiliary methodology --- both techniques were described as "the second best way to do almost anything"
[[Miaoulis and Plemenos, 2008](#miaoulis2008intelligent);
[Eiben, 2015](#eiben2015introduction)].
However, the utility and ubiquity of ANNs has since increased dramatically.
The development of AlexNet is widely considered pivotal to this transformation.
AlexNet united methodological innovations from the field (such as big datasets, dropout, and ReLU) with GPU computing that enabled training of orders-of-magnitude-larger networks.
In fact, some aspects of their deep learning architecture were expressly modified to accommodate multi-GPU training [[Krizhevsky et al., 2012]](#krizhevsky2012imagenet).
By adapting existing methodology to exploit commercially available hardware, AlexNet spurred the greater availability of compute resources to the research domain and eventually the introduction of custom hardware to expressly support deep learning
[[Jouppi et al., 2017]](#jouppi2017datacenter).

Similarly, progress toward realizing artificial life systems with indefinite scalability seems likely to unfold as incremental achievements that spur additional interest and resources in a positive feedback loop with the development of methodology, software, and eventually specialized hardware to take advantage of those resources.
In addition to developing hardware-agnostic theory and methodology, we believe that pushing the envelope of open-ended evolution will analogously require designing systems that leverage existing commercially-available parallel and distributed compute resources at circumstantially-feasible scales.
Modern high-performance scientific computing clusters appear perhaps the best target to start down this path.
These systems combine memory-sharing parallel architectures comprising dozens of cores (commonly targeted using OpenMP
[[Dagum and Menon, 1998]](#dagum1998openmpi)
and low-latency high-throughput message-passing between distributed nodes (commonly targeted using MPI
[[Clarke et al., 1994]](#clarke1994mpi)).

Contemporary scientific computing clusters lack key characteristics required for indefinite scalability: fault tolerance and arbitrary extensibility.
However, they also may offer an opportunity not available in an indefinitely scalable framework: log-time interconnects [[Mollah et al., 2018]](#mollah2018comparative).

### Instantiating Small-World Networks on Parallel and Distributed Hardware

Many natural systems --- such as ecosystems, genetic regulatory networks, and neural networks --- are known to exhibit small-world patterns of connectivity or interaction among components
[[Bassett and Bullmore, 2017](#bassett2017small);
[Fox and Bellwood, 2014](#fox2014herbivores);
[Gaiteri et al., 2014](#gaiteri2014beyond)].
In small-world graphs, mean path length (the number of edges traversed on a shortest-route) between arbitrary components scales logarithmically with system size [[Watts and Strogatz, 1998]](#watts1998collective).
We anticipate that open-ended phenomena emerging across distributed hardware might also involve small-world connectivity dynamics.

What would the impact be of providing a system of hierarchical log-time hardware interconnects as opposed to relying solely on local hardware interconnects?

In Sections
[WAGSW](#wiring-a-generic-small-world-graph),
[WAISO](#wiring-an-ideal-space-filling-hierarchical-tree-without-log-time-physical-interconnects),
[WAISW](#wiring-an-ideal-space-filling-hierarchical-tree-with-log-time-physical-interconnects),
and [WAWSG](#wiring-a-watts-strogatz-graph),
we analyze the scaling relationship between system size and expected node-to-node hops traversed between computational elements interacting as part of an emergent small-world network.
[[Footnote WDWCM]](#footnote-wdwcm)

1. with and without hierarchical log-time physical interconnects between computational nodes, and
2. with computational nodes embedded on one-, two-, or three-dimensional computational meshes.

In [Section WAGSW](#wiring-a-generic-small-world-graph), we find that expected hops over edges weighted by edge betweenness centrality scales polynomially in all cases without hierarchical physical interconnects.
With hierarchical physical interconnects, a logarithmic scaling relationship can be achieved.

In Sections
[WAISO](#wiring-an-ideal-space-filling-hierarchical-tree-without-log-time-physical-interconnects),
[WAISW](#wiring-an-ideal-space-filling-hierarchical-tree-with-log-time-physical-interconnects)
we find that hierarchical physical interconnects yield better best-case mean hops per edge in the case of a one-dimensional computational mesh.
Interestingly, asymptotically better outcomes in two- and three- dimensional meshes cannot be guaranteed by hierarchical physical interconnects.
This suggests that --- even at truly vast scales --- emergent inter-component interaction networks could arise with bounded per-hardware-component messaging load.

In Section [WAWSG](#wiring-a-watts-strogatz-graph) we show that, with a specific traditional construction of small-world graphs, best-case mean hops per edge scales polynomially with graph size.
With hierarchical physical interconnects, a logarithmic scaling relationship can still be achieved.

These theoretical analyses suggest that whether log-time physical interconnects deliver asymptotically better mean connection latency and hop-efficiency depend on the structure of the network overlaid on a spatially-distributed hardware system.
Although we focus on asymptotic analyses, better scaling coefficients might be achieved with long-distance hardware interconnects.
Equivalent asymptotic behavior does not preclude important considerations with respect to performance.

### Exploiting Log-Time Physical Interconnects: a Case Study

What could an artificial life system that exploits log-time hardware interconnects look like?

We present an extension to the DISHTINY platform for studying evolutionary transitions in individuality [[Moreno and Ofria, 2019]](#moreno2019toward).
In previous work with the system, cells situated on a two-dimensional grid interact exclusively with immediate neighbors.
This extension introduces genetic programs that can explicitly-register direct interconnects between (potentially distant) cells for messaging and resource-sharing.
Cells establish these interconnects through a genetically-mediated exploratory growth process.

We report a case study of an evolved strain that adaptively employs interconnects to communicate and selectively distribute resources to the periphery of a multicellular organism.
In Section [CSIM](#case-study-interconnect-messaging), we report another case study of an evolve strain that adaptively employs over-interconnect messaging to selectively suppress somatic cell reproduction.

In future implementations, explicitly-registered cell-cell interconnects may use log-time physical interconnects.
Our prototype implementation exploits shared-memory thread-level parallelism on a single multiprocessor.

### Abstraction, Engineering, and Computational Scale

Although designed with an eye toward scalability, largely along the lines outlined by Ackley, DISHTINY exchanges a uniform, evolutionary-passive substrate for manually-engineered self-replicating cells.
Evolutionary transitions in individuality provide a framework to unite self-replicators and induce meaningful functional synthesis of programmatic components tied to individual compute elements.
This approach mirrors the philosophy of practicality and feasibility laid out by Channon [[Channon, 2019]](#channon2019maximum):

> It is not computationally feasible (even if we knew how) for an OEE simulation to start from a sparse fog of hydrogen and helium and transition to a biological-level era, so it is clearly necessary to skip over or engineer in at least some complex features that arose through major transitions in our universe.

DISHTINY engineers-in some complex features (e.g., cellular structure, genetic transmission of variation, explicitly-registered cell-cell interconnects) in a manner that aims to reflect underlying hardware capabilities (e.g., procedural expression of programs, log-time physical interconnects) so they can be fully utilized.

More granular, less prescriptional approaches seem likely to become preferred when orders of magnitude of more compute power --- toward the extent envisioned by Ackley --- become available.
Such systems will address important questions in their own right about the computational foundations of physical and biological reality.
Current work developing those systems sets the stage for that eventuality [[Ackley, 2018]](#ackley2018digital).

## Methods

Our evolutionary case studies employ an extension to the DISHTINY framework for studying fraternal transitions in individuality.
'Initial work with this system characterized selective pressures for cooperation with kin [[Moreno and Ofria, 2019]](#moreno2019toward).
We have since extended the system to use the SignalGP event-driven genetic programming technique [[Lalejini and Ofria, 2018]](#lalejini2018evolving) to control cell behaviors.
Diverse multicellular life histories evolved in SignalGP-enabled DISHTINY evolutionary trials, involving reproductive division of labor, resource sharing (including, in some treatments, endowment of offspring groups), asymmetrical within-group and inter-group phenomena mediated by cell-cell messaging, morphological patterning, gene-regulation mediated life cycles, and adaptive apoptosis [[Moreno and Ofria, prep]](#dishtinygp).

DISHTINY simulates individual cells, each of which occupies a tile on a toroidal grid.
Cells can reproduce, placing daughter cells into adjoining tiles.
We allow cells the opportunity to engage with kin in a cooperative resource-collection task (Supplementary Section A), which can increase their individual cellular reproduction rates [[Moreno and Ofria, 2020]](#Moreno_Ofria_2020).
Kin groups are explicitly registered: on birth, a cell is either added to its parents group or expelled to establish a new group (Supplementary Section B) [[Moreno and Ofria, 2020]](#Moreno_Ofria_2020).

Cells can differentiate between neighbors that are members of their kin group and neighbors that are not and alter their behavior accordingly.
Each cell contains four SignalGP instances (all executing the same genetic program), one of which controls cell behavior with respect to each neighbor.
These instances may communicate with one another by means of intracellular messaging.
In this work, we add a fifth SignalGP instance to the DISHTINY cell.
This instance can execute special instructions to establish long-distance interconnects with other cells and engage in resource-sharing and/or message passing with those cells.
[Figure AOSHW](#fig-aoshw) summarizes how SignalGP hardware is arranged within DISHTINY cells.

![Arrangement of SignalGP hardware within DISHTINY cells](/resources/practical-scalability-1.png){:style="width: 100%; max-width: 500px; margin-left: auto; margin-right: auto; display: block;"}
[**Figure AOSHW:**](#fig-aoshw){:id="fig-aoshw"}
_Arrangement of SignalGP hardware within DISHTINY cells (gray squares).
Neighbor-managing hardware (circles) receive stimuli and control cell behavior with respect to a particular cell neighbor.
Network-managing hardware (interior squares) receive stimuli and control cell
behavior with respect to more distant neighbors a cell has established interconnects with._

Long-distance interconnects are established through a developmental process, summarized in [Figure IOTDP](#fig-iotdp).
The process begins with the placement of two independent search prongs at the originating cell.
Each prong performs a random walk over the originating cell's kin group, accumulating positive or negative feedback based on tags expressed by underfoot cells.
If a prongs accumulates positive feedback too slowly, it is reset to the location of the better-scoring prong.
Once a positive feedback threshold has been reached, the best-scoring prong develops into a full-fledged connection.
At this point, the originating cell can begin exchanging messages and/or resource over the connection.
Established interconnects may be subsequently removed by either participating cell.

Full details on hardware-level instructions and event-driven environmental cues available to cells are provided in Supplementary Sections D, E, F, and G [[Moreno and Ofria, 2020]](#Moreno_Ofria_2020).

![Illustration of the developmental processe used to establish long-distance interconnects](/resources/practical-scalability-2.png){:width="100%"}
[**Figure IOTDP:**](#fig-iotdp){:id="fig-iotdp"}
_Illustration of the developmental process used to establish long-distance interconnects.
Cells start by budding developmental search prongs (a) that perform a random search (b), reverting to the most successful search (c) where it matures to establish a connection (d).
Messages and resources can be transmitted over a connection (e) until either cell decides to terminate the connection (f). You can see this developmental process in action in an evolved strain at [`https://mmore500.com/hopto/ap`](https://mmore500.com/hopto/ap)._

### Evolutionary Screens

Our evolutionary screens consisted of 64 independent evolutionary batches.
We processed each batch in four-hour epochs to enable efficient job scheduling.
Each batch consisted of four isolated 45-by-45 toroidal subpopulations.
Subpopulations were completely intermixed in between four-hour steps.
To facilitate evolutionary search, in addition to a base mutation rate applied to cell division, additional mutations were applied to cells seeding a toroidal grid at the outset of an epoch or budding to form new kin groups during an epoch.

We screened across four-hour checkpoints of replicate batches to see if messages or resource were being sent over interconnects.
We sampled from these populations, performing screens for knockouts of over-interconnect messaging or resource sharing.
We then performed a secondary screen on strains with adaptive over-interconnect messaging or resource sharing to determine if re-routing either messages or shared resources decreased fitness.

We measured relative fitness using competition experiments between strains.
For some competition experiments reported in the case studies, we provide hyperlinks to load a in-browser DISHTINY simulation with the actual strains that were used.
In this web viewer, wild-type strains carry phylogentic root ID 1 and knockout strains carry ID 2.

### Implementation

We implemented our experimental system using the Empirical library for scientific software development in C++, available at [`https://github.com/devosoft/Empirical`](https://github.com/devosoft/Empirical) [[Ofria et al., 2019]](#charles_ofria_2019_2575607).
We used OpenMP to parallelize our main evolutionary replicates, distributing work over two threads.
The code used to perform and analyze our experiments, our figures, data from our experiments, and a live in-browser demo of our system is available via the Open Science Framework at [`https://osf.io/53vgh/`](https://osf.io/53vgh/) [[Foster and Deardorff, 2017]](#foster2017open).

## Case Study: Interconnect Resource Sharing

![](/resources/practical-scalability-3a.png){:style="width: 100%;"}
_(a) Hypothesized resource-recruiting mechanism_

![](/resources/practical-scalability-3b.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(b) Kin groups_

![](/resources/practical-scalability-3c.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(c) Established interconnects_

![](/resources/practical-scalability-3d.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(d) Spatial distribution of resource-sending cells_

![](/resources/practical-scalability-3e.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(e) Spatial distribution of resource-receiving cells_

[**Figure B42CS:**](#fig-b42cs){:id="fig-b42cs"}
_Batch 42 case study overview.
Figures 3b through 3e are generated from a snapshot of a wild-type strain monoculture population.
In these images, each grid tile represents an individual cell.
Cells are organized into kin groups, color-coded by hue in Figure B42CS(b).
Established interconnects are overlaid in blue on Figure B42CS(c).
In Figures B42CS(d) and B42CS(e), kin groups are outlined in black.
Figure B42CS(d) highlights cells that are sending resource over-interconnect.
Figure B42CS(e) highlights cells that are receiving resource over-interconnect.
You can view an animation of the wild-type monoculutre at [`https://mmore500.com/hopto/ao`](https://mmore500.com/hopto/ao)._


This case study was drawn from epoch 24 of batch 42 of the initial set of evolutionary runs.
We initially considered it for further study due to the presence of widespread over-interconnect resource sharing.
After preliminary knockout experiments confirmed the adaptive significance of both over-interconnect resource-sharing and over-interconnect messaging, we set aside the strain for a case study.
The evolutionary history preceding this case study consumed approximately 96 hours of wall-clock time and 736 compute-core hours.
Approximately 30 million simulation updates and 40,000 cellular generations elapsed.
You can view the strain this case study characterizes in a live in-browser simulation at [`https://mmore500.com/hopto/8`](https://mmore500.com/hopto/8).

Our first step was to evaluate whether the intercellular nature of over-interconnect messaging and resource sharing contributed to this strain's fitness.
(It is possible that messaging and/or resource sharing behaviors might generate stimuli on the recipient or side-effects on the sender that have adaptive consequences whether or not the sender and recipient are distinct cells;
in such a scenario, cells would be just as well off sending messages and/or resource to themselves.)
We performed several competition experiments between the wild-type strain and variants where interconnect messaging and resource sharing was altered to be intracellular instead of intercellular.
At the end of competition experiments, we evaluated the relative abundances of wild-type and variant strains.
In the first variant strain we tested, all outgoing over-interconnect messages were instead delivered to the sending cell.
In 16 out of 16 one-hour competition runs that were seeded half-and-half with the wild-type and variant strains, the wild-type strain drove the variant strain to extinction (one-tailed binomial test; $$p < 0.0001$$; 290 S.D 17 cell gens elapsed).
We observed a similar outcome with a second variant strain where all outgoing over-interconnect resource sharing was rerouted back to the sending cell (14/16 variant strain extinctions; 16/16 wild-type prevalence; 289 S.D. 25 cell gens elapsed).
Finally, a third variant strain where both over-interconnect messaging and over-interconnect resource sharing were returned to the sending cell exhibited the same outcome (16/16 variant strain extinctions; 300 S.D. 23 cell gens elapsed).
The intercellular natures of both over-interconnect messaging and resource sharing appear essential to fitness.

Next, we took a closer look at the evolved cellular mechanisms controlling over-interconnect messaging and resource sharing.
We monitored hardware execution of the wild-type strain in a monoculture population to detect which signals, messages, and fork/call instructions activated each SignalGP module.
We manually cross-referenced this information with a human-readable printout of the strain's genetic program to construct a hypothesized mechanism shown in [Figure B42CS](#fig-b42cs).
We hypothesize that cells at the periphery of a registered kin groups send messages backwards over incoming interconnects that induce interconnect-originating cells to send them resource.
Such a mechanism could preferentially increase resource availability at the group periphery, a region where cell-cell conflict is likely elevated.

We performed a series of four-hour competition experiments between wild type and knockout strains to confirm the adaptive significance of each component of this mechanism.
We began by re-routing stimulus 19, which alerts cells to neighbors that are members of a foreign kin group, to activate a known no-op module.
This knockout strain experienced decreased fitness compared to the wild-type strain (16/16 knockout strain extinctions; one-tailed binomial test; $$p < 0.0001$$; 1996 S.D. 280 cell gens elapsed; [`https://mmore500.com/hopto/ak`](https://mmore500.com/hopto/ak)).
Next, we replaced the over-interconnect messaging instruction that triggers over-interconnect resource-sharing with a no-op instruction.
This knockout strain also experienced decreased fitness (16/16 knockout strain extinctions; 1932 S.D. 223 cell gens elapsed; [`https://mmore500.com/hopto/al`](https://mmore500.com/hopto/al)).
We then replaced all eight copies of the over-interconnect resource-sharing instruction triggered by the over-interconnect messaging with no-op instructions, once more yielding a strain with diminished fitness (16/16 knockout strain extinctions; 1860 S.D. 370 cell gens elapsed; [`https://mmore500.com/hopto/am`](https://mmore500.com/hopto/am)).
Finally, we confirmed the soundness of our fitness competition methodology by running control wild-type versus wild-type competitions.
As expected, we observed no effect of strain ID on competition dominance (8/16 knockout strain extinctions; 8/16 wild-type strain extinctions; one-tailed binomial test; $$p = 0.60$$; 1738 S.D. 217 cell gens elapsed; [`https://mmore500.com/hopto/aj`](https://mmore500.com/hopto/aj)).

## Case Study: Interconnect Messaging

![](/resources/practical-scalability-4a.png){:style="width: 100%;"}
_(a) Hypothesized selective reproduction pausing mechanism_

![](/resources/practical-scalability-4b.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(b) Kin groups_

![](/resources/practical-scalability-4c.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(c) Established interconnects_

![](/resources/practical-scalability-4d.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(d) Spatial distribution of stimulus 5_

![](/resources/practical-scalability-4e.png){:style="width: 100%; max-width: 250px; margin-left: auto; margin-right: auto; display: block;"}
_(e) Spatial distribution of module 14 execution_

[**Figure B32CS:**](#fig-b32cs){:id="fig-b32cs"}
_Batch 32 case study overview.
Figures B32CS(b) through B32CS(e) are generated from a snapshot of a wild-type strain monoculture population.
In these images, each grid tile represents an individual cell.
Cells are organized into kin groups, color-coded by hue in Figure B32CS(b).
Established interconnects are overlaid in blue on Figure B32CS(c).
In Figures B32CS(d) and B32CS(e), kin groups are outlined in black.
Figure B32CS(d) highlights cells that are sending resource over-interconnect.
Figure B32CS(e) highlights cells that are receiving resource overinterconnect.
You can view an animation of the wild-type monoculutre at [`https://mmore500.com/hopto/an`](https://mmore500.com/hopto/an)._


This case study was drawn from epoch 18 of batch 32 from a secondary set of 64 evolutionary runs.
These runs were identical to the first, except:
* increasing the default outgoing connection cap,
* making cells default-accept instead of default-reject intracellular messages from same-channel cells, and
* removing system-mediated parent-kin-group recognition to promote kin group turnover.

We set this strain aside for case study after preliminary screening suggested that over-interconnect messaging played an adaptive role and that the intercellular nature the messaging of was necessary to that adaptation.
The evolutionary history preceding this case study consumed approximately 72 hours of wall-clock time and 576 compute-core hours.
Approximately 2,197,976 simulation updates and 8,884 cellular generations elapsed.
You can view this case study strain in a live in-browser simulation at [`https://mmore500.com/hopto/7`](https://mmore500.com/hopto/7).

As before, we began by testing whether over-interconnect interaction was adaptive because of its intercellularity.
We performed a competition experiment between the wild-type strain and a variant where over-interconnect messages were re-routed back to the sender.
[[Footnote TWAIR]](#foot-twair)
The wild-type strain was present in greater abundance at the end of all 16 competitions (one-tailed binomial test; $$p < 0.0001$$; 2/16 variant strain extinctions; 52 S.D. 3 cell gens elapsed).
So the adaptiveness of over-interconnect messaging does depend on the intercellular nature of that messaging in this strain.

We proceeded to tease apart the evolved cellular mechanisms this messaging interacts with.
We monitored hardware execution of the wild-type strain in a monoculture population to detect which signals, messages, and fork/call instructions activated each SignalGP module. %shorten because we already said it
% put in common things into case study introduction
Referring to a human-readable printout of the strain's evolved genetic programming, we pieced together the hypothesized mechanism shown in [Figure B32CS](#fig-b32cs).
It appears that neighboring a direct cellular offspring stimulates dispatch of an over-interconnect message that induces the recipient to pause somatic reproduction.

Four-hour competition experiments between wild type and knockout strains allowed us to assess the adaptiveness of each component of this mechanism.
We replaced the instruction responsible for over-interconnect messaging with a no-op instruction and observed a corresponding fitness penalty (16/16 knockout strain extinctions; one-tailed binomial test; $$p < 0.0001$$; 416 S.D. 58 cell gens elapsed; [`https://mmore500.com/hopto/aa`](https://mmore500.com/hopto/aa)).
We also replaced the reproduction-pausing instruction executed in response to over-interconnect messaging with a no-op.
This caused a similar fitness penalty (16/16 knockout strain extinctions; 401 S.D. 29 cell gens elapsed).

To double-check whether messaging specifically over interconnects was key to adaptivity we also competed the wild-type strain against variants with the focal over-interconnect messaging instruction substituted for all other possible module-activating instructions:
* call (378 S.D. 42 cell gens elapsed; [`https://mmore500.com/hopto/ac`](https://mmore500.com/hopto/ac))
* fork (377 S.D. 37 cell gens elapsed; [`https://mmore500.com/hopto/ad`](https://mmore500.com/hopto/ad))
* internal message send (406 S.D. 39 cell gens elapsed; [`https://mmore500.com/hopto/ae`](https://mmore500.com/hopto/ae))
* internal message send-to-all (422 S.D. 30 cell gens elapsed; [`https://mmore500.com/hopto/af`](https://mmore500.com/hopto/af))
* external message send (377 S.D. 37 cell gens elapsed; [`https://mmore500.com/hopto/ag`](https://mmore500.com/hopto/ag))
* external message send-to-all (440 S.D. 32 cell gens elapsed; [`https://mmore500.com/hopto/ah`](https://mmore500.com/hopto/ah))

In each case the substitution variant strain was driven to extinction across all 16 replicate experiments (one-tailed binomial test; $$p < 0.0001$$).

The directionality of messaging over the interconnect, however, does not appear to affect fitness.
We tried substituting the wild-type instruction, which dispatches a message from the terminus of an interconnect to its origin, with an instruction that instead dispatches a message from the origin of an interconnect to its terminus.
In competition against wild-type, the wild type strain was more abundant in only ten of 16 replicate competitions (one-tailed binomial test; $$p = 0.2272$$; 14/16 coalesced to a single strain; 410 S.D. 50 cell gen; [`https://mmore500.com/hopto/ai`](https://mmore500.com/hopto/ai}).

Next we assessed the adaptiveness of the particular spatio-temporal pattern of stimulation induced by incoming over-interconnect  messages.
Does this pattern differ from spatially and temporally random stimulation?
If it does, is the non-uniformity of stimulation adaptive?
To assess these questions, we measured the fraction of cells expressing module 14 in a monoculture wild-type population.
Then, we created a variant strain where outgoing over-interconnect messages from module 5 were disabled and, instead, module 14 activated randomly with probability based on the empirical wild-type activation rate.
[[Footnote BOIBM]](#foot-boibm)
<!-- % between updates 1000 and 1100 updates 40659 paused, 64641 not paused
% 40659/105200 0.3864 paused -->

In effect, this manipulation decouples reproductive pause from the distribution of over-interconnect message delivery and instead couples it to a comparable uniform random distribution.
Indeed, in competition experiments against the wild-type strain this variant fares poorly (15/16 wild-type strain prevalent; 0 variant strain extinctions; one-tailed binomial test; $$p < 0.001$$; 36 S.D. 2 cell gens elapsed), suggesting that the pattern of stimulation induced by over-interconnect messaging is meaningfully non-uniform.
We confirmed this result with a larger-scale set of competition trials (58/64 wild-type strain prevalent; 0 strain extinctions; one-tailed binomial test; $$p < 0.0001$$; 33 S.D. 2 cell gens elapsed).

Does the adaptively non-uniform pattern of stimulation induced by over-interconnect messages depend on non-uniform dispatch of messages from sending cells?
To assess, this question, we measured the per-cell frequency of module 5 activation in a monoculture wild-type population.
We then created a variant strain where outgoing over-interconnect messages from module 5 were disabled.
Instead, the over-interconnect message instruction was randomly executed with uniform per-cell probability based on the empirical wild-type execution rate.
This variant strain held its own against the wild-type strain (5/16 wild-type strain prevalent; 0 strain extinctions; one-tailed binomial test; $$p = 0.9$$; 30 S.D 1 cell gens elapsed).
So, this strain's non-uniform pattern of stimulation seems likely to a result from the actual pattern of cell-cell interconnection rather than selective message dispatch.

We did not find evidence that cells were using tag-based developmental attractors or repulsors to bias connectivity (5/16 wild-type strain prevalent; 0 strain extinctions; $$p=0.9$$; 35 S.D. 8 cell gens elapsed).
However, we did notice frequent interconnect turnover via execution of both remove-incoming and remove-outgoing interconnect instructions.
Substituting these instructions for no-ops yielded a knockout strain with lower fitness than wild-type (13/16 wild-type strain prevalent; 0 strain extinctions; one-tailed binomial test; $$p < 0.05$$; 30 S.D. 11 cell gens elapsed).
We confirmed this result with a larger-scale set of competition trials (60/64 wild-type strain prevalent; 0 strain extinctions; one-tailed binomial test; $$p < 0.0001$$; 39 S.D. 5 cell gens elapsed).
Is this remodeling of connectivity adaptively non-uniform?
We measured the interconnect removal rate in a monoculture wild-type population.
Then, we created a variant strain where interconnect-removal instructions were disabled.
Instead, interconnects in this strain were removed randomly with uniform probability.
In head-to-head competitions, this variant strain did not exhibit diminished fitness (20/64 wild-type strain prevalent; 0 strain extinctions; one-tailed binomial test; $$p = 1.0$$; 30 S.D. 2 cell gens elapsed).

The adaptive mechanism of over-interconnect messaging at play in this strain remains somewhat unclear.
Over-interconnect messaging induces an adaptively non-uniform pattern of module 14 activation.
The transmission of messages *between* cells over the interconnects, in particular, contributes to fitness.
When messages that would be delivered over interconnects are instead re-routed to the sending cell, fitness decreases.
Substituting over-interconnect messaging for local messaging also decreases fitness.
However, message dispatch is effectively random.
This strain employs an adaptive during-lifetime interconnect-remodeling scheme.
However, this remodeling scheme is also effectively random.

Although the process of interconnect development and retention might contribute some sort of spatial and/or temporal bias to module 14 activation, a full characterization of the nature of this bias and the mechanism inducing remains elusive.

## Wiring a Generic Small World Graph

Consider a set of computational nodes arranged in an $$r$$-dimensional mesh.
In each dimension, physical interconnects run between immediately adjacent pairs of nodes.
Represent this physical hardware with a graph $$N$$.
Vertices of $$N$$, $$V(N)$$, represent computational nodes.
Edges of $$N$$, $$E(N)$$, represent physical interconnects between nodes.

Let $$d(a,b)$$ represent the typical number of physical interconnects traversed on a shortest path between a pair of arbitrary nodes $$a, b \in V(N)$$.
This is conceptually equivalent to Manhattan distance.

In the case of a one-dimensional sequence of nodes, for a pair of arbitrary nodes $$a,b \in V(N)$$,
<div>
\begin{equation}
\bar{d}(a,b) \propto |V(N)|.
\end{equation}
</div>

Consider next the case of a higher-dimensional grid topology, like a two-dimensional grid or a three-dimensional mesh.
Because $$d$$ is a Manhattan metric, the number of physical interconnects requiring traversal in each dimension on a shortest-path between two nodes is completely independent.

Arranging the set of nodes $$N$$ in a $$r$$-dimensional cube, cube width in each dimensions scales proportionally to the $$r$$-th root of <span>$$|V(N)|$$</span>.

So, for a pair of arbitrary nodes $$a,b \in V(N)$$,
<div>
\begin{equation*}
\bar{d}(a, b) \propto |V(N)|^{\frac{1}{r}} \times r.
\end{equation*}
</div>

We proceed to construct a small world directed graph $$G$$ using the set of nodes $$N$$ as vertices.
In formal terms, a bijective relationship $$f: V(N) \rightarrow V(G)$$ unites these two sets.
The inverse mapping, $$f^{-1}: V(G) \rightarrow V(N)$$, is also bijective.

Edges in the graph $$G$$ do not represent a physical interconnect.
Instead, edges $$\{\hat{a}, \hat{b}\} \in E(G)$$ represent a close-coordination relationship where node $$\hat{a}$$ frequently interacts with (i.e., dispatches messages to) the destination node $$\hat{b}$$.
[Figure RBACM](#fig-rbacm) illustrates the relationship between $$N$$ and $$G$$.

Let $$\hat{d}(\hat{a},\hat{b})$$ denote distance between vertices $$\hat{a}$$ and $$\hat{b}$$ with respect to the graph $$G$$.
That is, the number of graph edges traversed on a shortest-path route between $$\hat{a}$$ and $$\hat{b}$$ over $$G$$.
In a small-world network, typical graph distance scales proportionally with the logarithm of network size [[Watts and Strogatz, 1998]](#watts1998collective).
In our case, for arbitrary $$\hat{a},\hat{b} \in V(G)$$,
<div>
\begin{equation} \label{eqn:smallworld_prop}
\bar{\hat{d}}(\hat{a},\hat{b}) \propto \log(|V(G)|).
\end{equation}
</div>

Consider the sequence of edges in $$G$$ traversed on a shortest-path route $$R_{\hat{a},\hat{b}}$$ between $$\hat{a}, \hat{b} \in V(G)$$, $$\{\{\hat{v}_1, \hat{v}_2\}, \{\hat{v}_2, \hat{v}_3\}, \ldots, \{\hat{v}_{n-1}, \hat{v}_n\} \}$$.
If we traverse these same nodes over the graph $$N$$ this path would be at least as long as the direct path between $$f^{-1}(\hat{a})$$ and $$f^{-1}(\hat{b})$$ over $$N$$.
(Otherwise, we would violate the Manhattan metric on $$N$$'s triangle inequality.)
Therefore,
<div>
\begin{equation} \label{eqn:path_hops_inequality}
\sum_{\{\hat{v}_i, \hat{v}_{i+1}\} \in  R_{\hat{a},\hat{b}}}
\Big[ d\Big(f^{-1}(\hat{v}_i), f^{-1}(\hat{v}_{i+1})\Big) \Big]
\geq
d\Big(f^{-1}(\hat{a}), f^{-1}(\hat{b})\Big).
\end{equation}
</div>

Recall that $$\hat{a},\hat{b}$$ are sampled uniformly from $$V(G)$$.
So, $$f^{-1}(\hat{a}),f^{-1}(\hat{b})$$ are sampled uniformly from $$V(N)$$.
Thus, Equation \ref{eqn:mesh_prop} allows us to establish the following lower bound,
<div>
\begin{equation*}
d\Big(f^{-1}(\hat{a}), f^{-1}(\hat{b})\Big)
\in
\Omega \Big(
  |V(N)|^{\frac{1}{r}} \times r
\Big).
\end{equation*}
</div>

It follows from Inequality \ref{eqn:path_hops_inequality} that
<div>
\begin{equation*}
\sum_{\{\hat{x}, \hat{y}\} \in  R_{\hat{a},\hat{b}}}
\Big[ d\Big(f^{-1}(\hat{x}), f^{-1}(\hat{y})\Big) \Big]
\in
\Omega \Big(
  |V(N)|^{\frac{1}{r}} \times r
\Big).
\end{equation*}
</div>

Equation \ref{eqn:smallworld_prop} tells us that the mean number of edges in $$R_{\hat{a}, \hat{b}}$$ is proportional to $$\log(|V(G)|)$$.
So, letting $$\bar{d}$$ represent the mean case,
<div>
\begin{equation*}
\log(|V(G)|) \times \bar{d}\Big(f^{-1}(\hat{x}), f^{-1}(\hat{y})\Big)
\in
\Omega \Big(
  |V(N)|^{\frac{1}{r}} \times r
\Big).
\end{equation*}
</div>

Rearranging and simplifying, we arrive at a lower bound of mean distance over the Manhattan network $$N$$ traversed for a connection in the interaction network $$G$$,
<div>
\begin{equation*}
\bar{d}\Big(f^{-1}(\hat{x}), f^{-1}(\hat{y})\Big)
\in
\Omega \Big(
  \frac{
    |V(N)|^{\frac{1}{r}} \times r
  }{
    \log(|V(N)|)
  }
\Big).
\end{equation*}
</div>

Note that edges $$\{\hat{x},\hat{y}\}$$ are not sampled uniformly from $$E(G)$$.
Instead, their sampling is weighted by edge betweenness centrality.
[[Footnote CAPON]](#foot-capon)

## Wiring an Ideal Space-Filling Hierarchical Tree without Log-Time Physical Interconnects

Consider, again, a set of computational nodes arranged in an $$r$$-dimensional mesh.
In each dimension, physical interconnects run between immediately adjacent pairs of nodes.
Let this physical hardware corresponds to a graph $$N$$ where $$V(N)$$ represents computational nodes and $$E(N)$$ represents physical interconnects between nodes.

Let $$d(a,b)$$ represent the typical number of physical interconnects traversed on a shortest path between a pair of arbitrary nodes $$a, b \in V(N)$$.
This is conceptually equivalent to Manhattan distance.

Suppose we have a small-world graph $$G$$ with maximum vertex degree bounded by a finite constant $$m$$.
The vertices of this graph $$G$$ are embedded one-to-one on $$N$$ such that $$|V(G)| = |V(N)|$$.
(Again, along the lines of [Figure RBACM](#fig-rbacm).)


Pick an arbitrary vertex $$a \in V(G)$$.
By the definition of a small-world graph,
<div>
\begin{equation*}
  \frac{1}{|V(G)|} \sum_{v \in V(G)} d(a, v) \propto \log |V(G)|.
\end{equation*}
</div>

Because the degree of the graph $$G$$ is bounded by $$m$$, there must be a subset $$T \subseteq G$$ that, for some branching factor $$k \geq 2$$ forms a complete $$k$$-nary tree rooted at $$a$$ such that
1. the tree height of $$T$$ is <span>$$h \propto \log |V(G)|$$</span> and
2. <span>$$|V(T)| \propto |V(G)|$$</span>.

[Legenstein and Maass](#legenstein2001optimizing) establish a lower bound for the length of wiring required to construct a $$k$$-nary tree with $$n$$ nodes on a one-dimensional $$L_1$$ grid,
<div>
\begin{equation*}
\Omega(n \log n).
\end{equation*}
</div>

In our case, this corresponds to the total number of hops over $$N$$ to traverse every edge in $$T$$.
Because, $$T \subseteq G$$, $$\Omega(n \log n)$$ is also a best-case lower bound for the total number of hops over $$N$$ to traverse every edge in $$G$$.

Because the degree of vertices in $$V(T)$$ is bounded by $$k$$,
<div>
\begin{equation*}
|E(T)| \in O \Big( |V(T)| \Big).
\end{equation*}
</div>

In fact, because the degree of vertices in $$V(G)$$ is also bounded by $$m$$,
<div>
\begin{equation*}
|E(G)| \in O \Big( |V(G)| \Big).
\end{equation*}
</div>

Let the wiring cost of an edge $$\{x, y\}$$ in $$E(G)$$ refer to the number of hops over $$N$$ required to travel from $$x$$ to $$y$$.
The best-case average wiring cost per edge can be computed as the best-case total wiring cost divided by the worst-case number of edges.
For arbitrary $$\{x, y\} \in E(G)$$,
<div>
\begin{eqnarray*}
\bar{d}(x, y)
&\in& \Omega \Big( \frac{ |E(G)| \times \log |E(G)| }{ |E(G)| } \Big)\\
&\in& \Omega \Big( \log |E(G)| \Big).
\end{eqnarray*}
</div>

This result applies to all possible small-world graphs $$G$$ embedded on a one-dimensional computational mesh.

To tractably extend our analysis to three-dimensional meshes, rather than all small-world graphs we will specifically analyze the wiring cost of ideal space-filling trees [[Kuffner and LaValle, 2009]](#kuffner2009space).
This construction efficiently distributes elements of $$G$$ over $$N$$ with respect to wiring cost.
Although this construction potentially represents a lower bound on wiring cost, its optimality has not been concretely established.

For three dimensions, the total length of wiring required as a function of the number of nodes is
<div>
\begin{equation*}
w_3(n)
=
\sum_{i=1}^{\log_8 n} \Big[
  \frac{n}{8^i} % how many to draw
  \times
  \frac{3}{2} \times 8 \times 2^{i} % how big each one is
\Big].
\end{equation*}
</div>

Because
<div>
\begin{equation*}
\lim_{n \rightarrow \infty}
\frac{w_3(n)}{n} = 4,
\end{equation*}
</div>

we have $$w_3(n) \in \Theta \Big( n \Big)$$.
For an $$n$$-node tree, edge count $$|E(G)| \in \Theta \Big( |V(G)| \Big)$$.
So, average edge wiring cost remains constant as $$|V(G)|$$ scales.
Similar analysis concludes an equivalent result in the two-dimensional case.

## Wiring an Ideal Space-Filling Hierarchical Tree with Log-Time Physical Interconnects

Once more, we will work with a mesh of $$n$$ physical hardware nodes corresponding to a graph $$N$$ where $$V(N)$$ represents computational nodes and $$E(N)$$ represents physical interconnects between nodes.
In this case, in addition to physical interconnects between spatially adjacent nodes we will assume a system of hierarchical physical interconnects that allows log-hop traversal between nodes.

![Example construction of an ideal space-filling tree over a computational mesh](/resources/practical-scalability-5.png){:width="100%"}
[**Figure ECOAI:**](#fig-ecoai){:id="fig-ecoai"}
_Example construction of an ideal space-filling tree over a computational mesh._

Suppose we have a small-world graph $$G$$ with maximum vertex degree bounded by a finite constant $$m$$.
The vertices of this graph $$G$$ are embedded one-to-one on $$N$$ such that $$|V(G)| = |V(N)|$$.
We will specifically construct this graph as an ideal space-filling tree.
[Figure RBACM](#fig-rbacm) illustrates the relationship between $$N$$ and $$G$$.

As a property of this construction, <span>$$|E(N)| \propto |V(N)|$$</span>.

In the best case, where edges in $$E(G)$$ happen to correspond exactly to hierarchical physical interconnects $$E(N)$$, the average hops required per edge is 1.
However, in the worst case the average number of hops over $$N$$ required per edge in $$E(G)$$ is bounded by $$\log_m n$$.

What if, instead of routing all traffic through log-time hierarchical interconnects, we routed traffic between nodes less than $$\log_m n$$ apart through local grid-mesh interconnects?

In this case, we can bound worst-case total wiring cost by
<div>
\begin{equation*}
\sum_{l = 1}^{\log_2 \log_m n} % short edges
\Big[
  m^{\log_m n - l} % number of edges
  \times
  2^l % hop length
\Big]
+
\log_m n % number hops
\times
\sum_{l = \log_2 \log_m n }^{ \log_m n} % long edges
m^{\log_m n - l}.
\end{equation*}
</div>

For the space-filling tree on a one-dimensional mesh, we have $$m = 2$$.
Our upper bound on total wiring cost simplifies to
<div>
\begin{equation*}
w_2(n) =
n \times \log_2 \log_2 n
+
\log_2 n \times (n \times \log_n 4 - 1).
\end{equation*}
</div>

Because
<div>
\begin{equation*}
\lim_{n \rightarrow \infty}
\frac{
  w_2(n)
}{
  n \times \log_2 \log_2 n
}
= 1,
\end{equation*}
</div>
we have $$w_2(n) \in \Theta \Big( n \times \log_2 \log_2 n \Big)$$.
Because edge count $$|E(G)| \in \Theta \Big( n \Big)$$ we can establish the following upper bound on $$\bar{W}(n)$$ mean wiring cost per edge in $$|E(G)|$$ for the one-dimensional case,
<div>
\begin{equation*}
\bar{W}(n) \in \Omega\Big( \log_2 \log_2 n \Big).
\end{equation*}
</div>

What about the three-dimensional case?
For the space-filling tree on a three-dimensional mesh, we have $$m = 8$$.
Our upper bound on total wiring cost simplifies to
<div>
\begin{eqnarray*}
w_8(n)
=& &
\frac{n}{3}
\times (1 - 4^{ \log_2 \log_n 8 }) \\
& &+
\frac{
  (
    n \times 8^{
      \log_2 \log_n 64
    } - 1
  ) \times \log_8 n
}{7}.
\end{eqnarray*}
</div>

Because
<div>
\begin{equation*}
\lim_{n \rightarrow \infty}
\frac{
  w_8(n)
}{
  n
}
= \frac{1}{3},
\end{equation*}
</div>
we have $$w_8 \in \Theta \Big( n \Big)$$.
Once more, because edge count $$|E(G)| \in \Theta \Big( n \Big)$$ we can establish the following upper bound on $$\bar{W}(n)$$ mean wiring cost per edge for the three-dimensional case,
<div>
\begin{equation*}
\bar{W}(n) \in \Omega \Big( 1 \Big).
\end{equation*}
</div>

## Wiring a Watts-Strogatz Graph

Consider a set of computational nodes arranged in an $$r$$-dimensional mesh.
In each dimension, physical interconnects run between immediately adjacent pairs of nodes.
Represent this physical hardware with a graph $$N$$.
Vertices of $$N$$, $$V(N)$$, represent computational nodes.
Edges of $$N$$, $$E(N)$$, represent physical interconnects between nodes.

Let $$d(a,b)$$ represent the typical number of physical interconnects traversed on a shortest path between a pair of arbitrary nodes $$a, b \in V(N)$$.
This is conceptually equivalent to Manhattan distance.

In the case of a one-dimensional sequence of nodes, for a pair of arbitrary nodes $$a,b \in V(N)$$,
<div>
\begin{equation*}
\bar{d}(a,b) \propto |V(N)|.
\end{equation*}
</div>

Consider next the case of a higher-dimensional grid topology, like a two-dimensional grid or a three-dimensional mesh.
Because $$d$$ is a Manhattan metric, the number of physical interconnects requiring traversal in each dimension on a shortest-path between two nodes is completely independent.

Arranging the set of nodes $$N$$ in a $$r$$-dimensional cube, cube width in each dimensions scales proportionally to the $$r$$-th root of <span>$$|V(N)|$$</span>.

So, for a pair of arbitrary nodes $$a,b \in V(N)$$,
<div>
\begin{equation} \label{eqn:mesh_prop}
\bar{d}(a, b) \propto |V(N)|^{\frac{1}{r}} \times r.
\end{equation}
</div>

We proceed to construct a small world directed graph $$G$$ using the set of nodes $$N$$ as vertices.
In formal terms, a bijective relationship $$f: V(N) \rightarrow V(G)$$ unites these two sets.
The inverse mapping, $$f^{-1}: V(G) \rightarrow V(N)$$, is also bijective.

![Relationship between a computational mesh N and a small-world interaction network G constructed over N](/resources/practical-scalability-6.png){:width="100%"}
[**Figure RBACM:**](#fig-rbacm){:id="fig-rbacm"}
_Relationship between a computational mesh $$N$$ and a small-world interaction network $$G$$ constructed over $$N$$._

Edges in the graph $$G$$ do not represent a physical interconnect.
Instead, edges $$\{\hat{a}, \hat{b}\} \in E(G)$$ represent a close-coordination relationship where node $$\hat{a}$$ frequently interacts with (i.e., dispatches messages to) the destination node $$\hat{b}$$.
[Figure RBACM](#fig-rbacm) illustrates the relationship between $$N$$ and $$G$$.

Let $$\hat{d}(\hat{a},\hat{b})$$ denote distance between vertices $$\hat{a}$$ and $$\hat{b}$$ with respect to the graph $$G$$.
That is, the number of graph edges traversed on a shortest-path route between $$\hat{a}$$ and $$\hat{b}$$ over $$G$$.
In a small-world network, typical graph distance scales proportionally with the logarithm of network size [[Watts and Strogatz, 1998]](#watts1998collective).
In our case, for arbitrary $$\hat{a},\hat{b} \in V(G)$$,
<div>
\begin{equation*}
\bar{\hat{d}}(\hat{a},\hat{b}) \propto \log(|V(G)|).
\end{equation*}
</div>

Suppose we have a small-world graph $$G$$ constructed over a mesh $$N$$ (as in [Figure RBACM](#fig-rbacm)) using the Watts–Strogatz algorithm.
In this procedure, vertices in $$V(G)$$ corresponding to neighboring computational nodes in $$V(N)$$ are wired together to form a lattice with mean degree $$k$$.
Then, for every vertex $$v \in V(G)$$, each edge $$\{x, y\} \in E(G)$$ containing $$v$$ is reconfigured with probability $$0 < \beta < 1$$ to connect $$v$$ to a randomly-chosen node $$w \in V(G)$$.

Before reconfiguration, the total wiring cost of $$G$$ with respect to hops over $$N$$ was proportional to <span>$$|V(G)|$$</span>.

Recall that, with mesh dimensionality $$r$$ we know that for a pair of arbitrary nodes $$a,b \in V(N)$$,
<div>
\begin{equation*}
\bar{d}(a, b) \propto |V(N)|^{\frac{1}{r}} \times r.
\end{equation*}
</div>

So, after rewiring, the total wiring cost $$w$$ of $$G$$ with respect to hops over $$N$$ can be calculated as
<div>
\begin{equation*}
  \beta |V(G)| \times |V(N)|^{\frac{1}{r}} \times r + (1 - \beta) |V(G)|.
\end{equation*}
</div>

So, <span>$$w \in \Omega \Big( |V(N)|^{\frac{r+1}{r}} \times r \Big)$$</span>.

In this graph, the number of edges is proportional to the graph size $$n$$.

With bounded mean degree, we have $$|E(G)| \propto |V(G)|$$ so we can establish the following lower bound on mean wiring cost per edge of $$G$$ with respect to hops over $$N$$,
<div>
\begin{equation*}
\Omega \Big( |V(G)|^{\frac{1}{r}} \times r \Big).
\end{equation*}
</div>

Note that, with the introduction of log-time hierarchical hardware interconnects into $$N$$ the mean wiring cost per edge of $$G$$ with respect to hops over $$N$$ is bounded in the worst case by <span>$$\Omega \Big( \log |V(G)| \Big)$$</span>.


## Conclusion

Ackley's concept of indefinite scalability lays out an ambitious vision for the computational substrate of future open-ended evolution models.
This vision has inspired researchers to incorporate thinking about underlying computational substrates into open-ended evolution theory and to consider how (or whether) available computational resources meaningfully constrain existing open-ended evolution models.
For the time being, computational substrates for open-ended evolution limited purely by physical (or economic) concerns remain on the horizon, but indefinite scalability has already had concrete, and fruitful, impact on thinking around open-ended evolution.

Although prevalent contemporary computational hardware (and the developer-facing software infrastructure that supports its use) lacks essential features necessary to achieve true indefinite scalability such as fault tolerance and purely relative addressing, many cores designed to support low-latency interconnects.
These high-performance computing resources are increasingly accessible.
Concern over indefinite scalability should not dissuade the design and implementation of open-ended evolution models that accommodate for the limitations of existing hardware and software infrastructure to make effective use of it.
We highlight how log-time hardware interconnects might be exploited in practically scalable, but other model design or implementation tradeoffs may be relevant too (e.g., model dynamics or performance gains that rely on absolute instead of purely relative addressing).

Realizing open-ended evolution models with truly vast computational substrates will require intermediate steps.
Efforts to pursue practical scalability that wrings out contemporary, commercially-available hardware and software infrastructure, will accelerate progress toward realizing truly indefinitely scalable systems.
It seems conceivable that, coupled with innovative model design informed by open-ended evolution theory and effective model implementation in code, contemporary hardware systems and software infrastructure harbor the potential to realize paradigm-shifting advances in open-ended evolution.
As was the case with deep learning, the tipping point of scale for model systems to exhibit qualitatively different behavior may be closer than we assume, perhaps only two or three orders of magnitude.

We highlighted how dynamic interactions within and between evolutionary individuals are crucial to open-ended evolution.
Open-ended evolution models designed to scale computationally should realize these dynamic interactions within a framework that can be efficiently and readily mapped onto parallel computational implementation.
Software tools that enable artificial life researchers to rapidly (and reusably) develop artificial life models have yielded substantial benefit to the field
[[Bohm and Hintze, 2017](#bohm2017mabe);
[Ofria et al., 2019](#charles_ofria_2019_2575607)].
Software tools or frameworks for parallel and distributed artificial life models that are versatile enough to support diverse use cases might help make practical scalability more practical.
In particular, tools to collect data on distributed evolving systems (especially systematics tracking) seem likely to benefit the community.

Here, we presented an extension of the DISHTINY framework as an example of an artificial life system that might hypothetically take advantage of log-time hardware interconnects.
We employed a very modest prototype parallel implementation that used shared-memory parallelism to distribute evolving --- and interacting --- populations of cells over two threads.
We provided a faculty for cells to establish long-distance interconnects over the computational mesh, which in future implementations could rely on hardware-level log-time interconnects.
We have characterized two strains that adaptively employed these interconnects to synthesize spatially-distributed functionality.
In the first case study, messaging and resource sharing over interconnects appeared to facilitate resource recruitment to multicell peripheries.
In a second case study, interconnect messaging played an adaptive role in selectively moderating somatic reproduction.

Incorporating simulation-level objects or physics in open-ended evolution models that explicitly correspond to hardware interconnects represents just one possible approach to exploiting them.
Automatic detection of emergent long-distance interactions across a computational mesh and dynamically re-routing signaling traffic to use hierarchical interconnects might also be possible.
Open-ended evolution models could also be entirely designed around hierarchical interconnects instead of a space-filling computational mesh.

At the core, from both the practical and indefinite standpoints, efforts to scale computational models of open-ended evolution, seek to realize the evolutionary generation of continually novel and increasingly complex artifacts.
As we scale DISHTINY, we are interested in assembling metrics to quantify different aspects of complexity in the system such as organization [[Goldsby et al., 2012]](#goldsby2012task), structure, and function [[Goldsby et al., 2014]](#goldsby2014evolutionary).
We believe that open-ended model systems built on contemporary distributed computational substrates will prove fruitful tools to investigate questions about how biological complexity relates to fitness, genetic drift over elapsed evolutionary time, mutational load, genetic recombination (sex and horizontal gene transfer), ecology, historical contingency, and key innovations.

## Let's Chat

I would love to hear your thoughts on scaling artificial life simulations and studying major transitions in evolution!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">nothing to see here, just a placeholder tweet 🐦</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1054071480512843776?ref_src=twsrc%5Etfw">October 21, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish: or make a comment :raising_hand_woman:

## Cite This Post

**APA**
> Moreno, M. A., & Ofria, C. (2020, June 25). Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution. https://doi.org/10.17605/OSF.IO/53VGH

**MLA**
> Moreno, Matthew A, and Charles Ofria. “Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution.” OSF, 25 June 2020. Web.

**Chicago**
> Moreno, Matthew A, and Charles Ofria. 2020. “Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution.” OSF. June 25. doi:10.17605/OSF.IO/53VGH.

**BibTeX**
```
@misc{Moreno_Ofria_2020,
  title={Practical Steps Toward Indefinite Scalability: In Pursuit of Robust Computational Substrates for Open-Ended Evolution},
  url={osf.io/53vgh},
  DOI={10.17605/OSF.IO/53VGH},
  publisher={OSF},
  author={Moreno, Matthew A and Ofria, Charles},
  year={2020},
  month={Jun}
}
```

## Footnotes

[Footnote WDWCM](#footnote-wdwcm){:id="footnote-wdwcm"}
Why do we consider mean node-to-node hops per connection?

Although relativistic concerns do ultimately limit latency between spatially-distributed computational elements, with respect to contemporary hardware co-located at a single physical site at foreseeable scales, we expect node-to-node hops to represent an important bottleneck on system performance.

At larger scales, consider the case where emergent connections are embodied via simulation state along the entire path of node-to-node hops traversed by the by the connection (along the line of axon wiring of biological neural networks).
If mean emergent connections per simulation element remain constant as the system scales, then mean node-to-node hops per connection relates to the amount of state required per node to represent connections that pass through it.
(Specifically, if mean node-to-node hops per connection remains constant than the amount of state required per node remains constant.)

Finally, the asymptotic analyses performed on mesh networks without long-distance hierarchical interconnects can be interpreted in terms of Euclidean distance.
(Potentially of interest with respect to relativistic limitations.)

[Footnote BOIBM](#foot-boibm){:id="foot-boibm"}
Because over-interconnect broadcast messages activate all hardware units of a cell, we selected entire cells randomly and activated module 14 on all hardware units.

[Footnote TWAOI](#foot-twaoi){:id="foot-twaoi"}
This was an independent replication of the initial experiment (performed as part of a wider screen) that singled out the case study strain for further analysis.

[Footnote CAPON](#foot-capon){:id="foot-capon"}
Consider all pairings of nodes in a graph.
Now, construct a multiset of paths that, for each possible node pairing, contains the shortest path between those two nodes.
Edge betweenness is the fraction of the paths in this mulitset that passes through a particular edge [[Lu and Zhang, 2013]](#Lu2013).

## References

<a
  href="https://doi.org/10.1162/isal_a_00021"
  id="ackley2018digital">
Ackley, D. H. (2018). Digital protocells with dynamic size, position, and topology. The 2018 Conference on Artificial Life: A Hybrid of the European Conference on Artificial Life (ECAL) and the International Conference on the Synthesis and Simulation of Living Systems (ALIFE), pages 83–90.
</a>

<a
  href="https://dl.acm.org/doi/10.5555/1991596.1991607"
  id="ackley2011pursue">
Ackley, D. H. and Cannon, D. C. (2011). Pursue robust indefinite scalability. In HotOS.
</a>

<a
  href="http://doi.org/10.1177/1073858416667720"
  id="bassett2017small">
Bassett, D. S. and Bullmore, E. T. (2017). Small-world brain networks revisited. The Neuroscientist, 23(5):499–516.
</a>

<a
  href="https://dl.acm.org/doi/10.5555/286139.286165"
  id="bedau1998classification">
Bedau, M. A., Snyder, E., and Packard, N. H. (1998). A classification of long-term evolutionary dynamics. In Artificial life VI, pages 228–237.
</a>

<a
  href="https://doi.org/10.1023/A:1010076532029"
  id="bedau1998classification">
Bennett III, F. H., Koza, J. R., Shipman, J., and Stiffelman, O. (1999). Building a parallel computer system for $18,000 that performs a half peta-flop per day. In Proceedings of the 1st Annual Conference on Genetic and Evolutionary Computation-Volume 2, pages 1484–1490. Citeseer.
</a>

<a
  href="https://patents.google.com/patent/US8918349B2"
  id="blondeau2012distributed">
Blondeau, A., Cheyer, A., Hodjat, B., and Harrigan, P. (2012). Distributed network for performing complex algorithms. US Patent App. 13/443,546.
</a>

<a
  href="https://doi.org/10.7551/ecal_a_016"
  id="bohm2017mabe">
Bohm, C. and Hintze, A. (2017). Mabe (modular agent based evolver): A framework for digital evolution research. In Artificial Life Conference Proceedings 14, pages 76–83. MIT Press.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00285"
  id="channon2019maximum">
Channon, A. (2019). Maximum individual complexity is indefinitely scalable in geb. Artificial life, 25(2):134–144.
</a>

<a
  href="https://doi.org/10.1109/SASP.2008.4570793"
  id="che2008accelerating">
Che, S., Li, J., Sheaffer, J. W., Skadron, K., and Lach, J. (2008). Accelerating compute-intensive applications with gpus and fpgas. In 2008 Symposium on Application Specific Processors, pages 101–107. IEEE.
</a>

<a
  href="https://doi.org/10.1007/978-3-0348-8534-8_21"
  id="clarke1994mpi">
Clarke, L., Glendinning, I., and Hempel, R. (1994). The mpi message passing interface standard. In Programming environments for massively parallel distributed systems, pages 213–218. Springer.
</a>

<a
  href="https://doi.org/10.1109/TEVC.2010.2104157"
  id="clune2011performance">
Clune, J., Stanley, K. O., Pennock, R. T., and Ofria, C. (2011). On the performance of indirect encoding across the continuum of regularity. IEEE Transactions on Evolutionary Computation, 15(3):346–367.
</a>

<a
  href="http://doi.org/10.1109/99.660313"
  id="dagum1998openmpi">
Dagum, L. and Menon, R. (1998). Openmp: an industry standard api for shared-memory programming. IEEE computational science and engineering, 5(1):46–55.
</a>

<a
  href="http://doi.org/10.7551/ecal_a_023"
  id="dolson2017spatial">
Dolson, E. and Ofria, C. (2017). Spatial resource heterogeneity creates local hotspots of evolutionary potential. In Artificial Life Conference Proceedings 14, pages 122–129. MIT Press.
</a>

<a
  href="https://proxy.lib.umich.edu/login?url=https://search.proquest.com/docview/2203009699?accountid=14667"
  id="dolson2019constructive">
Dolson, E. L. (2019). On the Constructive Power of Ecology in Open-Ended Evolving Systems. Michigan State University.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00280"
  id="dolson2019modes">
Dolson, E. L., Vostinar, A. E., Wiser, M. J., and Ofria, C. (2019). The modes toolbox: Measurements of open-ended dynamics in evolving systems. Artificial life, 25(1):50–73.
</a>

<a
  href="http://www.worldcat.org/oclc/1045691442"
  id="eiben2015introduction">
Eiben, A. and Smith, J. E. (2015). Introduction to evolutionary computing. Springer, Berlin.
</a>

<a
  href="http://doi.org/10.5195/jmla.2017.88"
  id="foster2017open">
Foster, E. D. and Deardorff, A. (2017). Open science framework (osf). Journal of the Medical Library Association: JMLA, 105(2):203.
</a>

<a
  href="https://doi.org/10.1111/1365-2435.12190"
  id="fox2014herbivores">
Fox, R. J. and Bellwood, D. R. (2014). Herbivores in a small world: network theory highlights vulnerability in the function of herbivory on coral reefs. Functional Ecology, 28(3):642–651.
</a>

<a
  href="http://doi.org/10.1111/gbb.12106"
  id="gaiteri2014beyond">
Gaiteri, C., Ding, Y., French, B., Tseng, G. C., and Sibille, E. (2014). Beyond modules and hubs: the potential of gene coexpression networks for investigating molecular mechanisms of complex brain disorders. Genes, brain and behavior, 13(1):13–24.
</a>

<a
  href="https://doi.org/10.1073/pnas.0701035104"
  id="gerhart2007theory">
Gerhart, J. and Kirschner, M. (2007). The theory of facilitated variation. Proceedings of the National Academy of Sciences, 104(suppl 1):8582–8589.
</a>

<a
  href="https://www.ibtimes.com/artificial-intelligence-here-help-you-pick-right-shoes-2144114"
  id="gilbert_2015">
Gilbert, D. (2015). Artificial intelligence is here to help you pick the right shoes.
</a>

<a
  href="https://doi.org/10.1073/pnas.1202233109"
  id="goldsby2012task">
Goldsby, H. J., Dornhaus, A., Kerr, B., and Ofria, C. (2012). Taskswitching costs promote the evolution of division of labor and shifts in individuality. Proceedings of the National Academy of Sciences, 109(34):13686–13691.
</a>

<a
  href="https://doi.org/10.1371/journal.pbio.1001858"
  id="goldsby2014evolutionary">
Goldsby, H. J., Knoester, D. B., Ofria, C., and Kerr, B. (2014). The evolutionary origin of somatic cells under the dirty work hypothesis. PLOS Biology, 12(5):e1001858.
</a>

<a
  href="http://doi.org/10.1109/HPCS.2007.17"
  id="harding2007fast">
Harding, S. and Banzhaf, W. (2007a). Fast genetic programming and artificial developmental systems on gpus. In 21st International Symposium on High Performance Computing Systems and Applications (HPCS’07), pages 2–2. IEEE.
</a>

<a
  href="https://dl.acm.org/doi/10.5555/1763756.1763766"
  id="harding2007fast2">
Harding, S. and Banzhaf, W. (2007b). Fast genetic programming on gpus. In European conference on genetic programming, pages 90–101. Springer.
</a>

<a
  href="http://www.worldcat.org/oclc/1105766939"
  id="hennessy2011computer">
Hennessy, J. L. and Patterson, D. A. (2011). Computer architecture: a quantitative approach. Elsevier.
</a>

<a
  href="https://patents.google.com/patent/US8527433B2/en"
  id="hodjat2013distributed">
Hodjat, B. and Shahrzad, H. (2013). Distributed evolutionary algorithm for asset management and trading. US Patent 8,527,433.
</a>

<a
  href="https://doi.org/10.2514/6.2006-7242"
  id="hornby2006automated">
Hornby, G., Globus, A., Linden, D., and Lohn, J. (2006). Automated antenna design with evolutionary algorithms. Space 2006.
</a>

<a
  href="https://doi.org/10.1145/1068009.1068297"
  id="hornby2005measuring">
Hornby, G. S. (2005). Measuring, enabling and comparing modularity, regularity and hierarchy in evolutionary design. In Proceedings of the 7th annual conference on Genetic and evolutionary computation, pages 1729–1736.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00263"
  id="huizinga2018emergence">
Huizinga, J., Stanley, K. O., and Clune, J. (2018). The emergence of canalization and evolvability in an open-ended, interactive evolutionary system. Artificial life, 24(3):157–181.
</a>

<a
  href="https://doi.org/10.1145/3140659.3080246"
  id="jouppi2017datacenter">
Jouppi, N. P., Young, C., Patil, N., Patterson, D., Agrawal, G., Bajwa, R., Bates, S., Bhatia, S., Boden, N., Borchers, A., et al. (2017). In-datacenter performance analysis of a tensor processing unit. In Proceedings of the 44th Annual International Symposium on Computer Architecture, pages 1–12.
</a>

<a
  href="https://doi.org/10.1073/pnas.95.15.8420"
  id="kirschner1998evolvability">
Kirschner, M. and Gerhart, J. (1998). Evolvability. Proceedings of
the National Academy of Sciences, 95(15):8420–8427.
</a>

<a
  href="https://www.ri.cmu.edu/publications/space-filling-trees/"
  id="kuffner2009space">
Kuffner, J. J. and LaValle, S. M. (2009). Space-filling trees. RI, Pittsburgh, PA, Tech. Rep. CMU-RI-TR-09-47
</a>

<a
  href="http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf"
  id="krizhevsky2012imagenet">
Krizhevsky, A., Sutskever, I., and Hinton, G. E. (2012). Imagenet classification with deep convolutional neural networks. In Advances in neural information processing systems, pages 1097–1105.
</a>

<a
  href="https://doi.org/10.1145/3205455.3205523"
  id="lalejini2018evolving">
Lalejini, A. and Ofria, C. (2018). Evolving event-driven programs with signalgp. In Proceedings of the Genetic and Evolutionary Computation Conference, pages 1135–1142.
</a>

<a
  href="https://doi.org/10.1162/isal_a_00191"
  id="langdon2019continuous">
Langdon, W. B. and Banzhaf, W. (2019). Continuous long-term evolution of genetic programming. In The 2018 Conference on Artificial Life: A Hybrid of the European Conference on Artificial Life (ECAL) and the International Conference on the Synthesis and Simulation of Living Systems (ALIFE), pages 388–395. MIT Press.
</a>

<a
  href="https://stars.library.ucf.edu/etd/2214/"
  id="lehman2012evolution">
Lehman, J. (2012). Evolution through the search for novelty.
</a>

<a
  href="https://doi.org/10.1162/EVCO_a_00025"
  id="lehman2011abandoning">
Lehman, J. and Stanley, K. O. (2011). Abandoning objectives: Evolution through the search for novelty alone. Evolutionary computation, 19(2):189–223.
</a>

<a
  href="https://doi.org/10.7551/978-0-262-31050-5-ch011"
  id="lehman2012beyond">
Lehman, J. and Stanley, K. O. (2012). Beyond open-endedness: Quantifying impressiveness. In Artificial Life Conference Proceedings 12, pages 75–82. MIT Press.
</a>

<a
  href="https://doi.org/10.1371/journal.pone.0062186"
  id="lehman2013evolvability">
Lehman, J. and Stanley, K. O. (2013). Evolvability is inevitable: Increasing evolvability without the pressure to adapt. PloS one, 8(4).
</a>

<a
  href="http://www.amsi.ge/jbpc/40707/40701.html"
  id="lipson2007principles">
Lipson, H. (2007). Principles of modularity, regularity, and hierarchy for scalable systems. Journal of Biological Physics and Chemistry, 7(4):125–128.
</a>

<a
  href="https://eccc.weizmann.ac.il/report/2001/069/"
  id="legenstein2001optimizing">
Legenstein, R. A. and Maass, W. (2001). Optimizing the layout of a balanced tree. In Electronic Colloquium on Computational Complexity (ECCC), volume 8.
</a>

<a
  href="https://doi.org/10.1007/978-1-4419-9863-7_874"
  id="Lu2013">
Lu, L. and Zhang, M. (2013). Edge Betweenness Centrality, pages 647–648. Springer New York, New York, NY.
</a>

<a
  href="https://doi.org/10.1073/pnas.0702207104"
  id="lynch2007frailty">
Lynch, M. (2007). The frailty of adaptive hypotheses for the origins of organismal complexity. Proceedings of the National Academy of Sciences, 104(suppl 1):8597–8604.
</a>

<a
  href="http://doi.org/10.1038/nature13570"
  id="markov2014limits">
Markov, I. L. (2014). Limits on fundamental limits to computation. Nature, 512(7513):147–154.
</a>

<a
  href="http://doi.org/10.1007/978-3-540-92902-4_1"
  id="miaoulis2008intelligent">
Miaoulis, G. and Plemenos, D. (2008). Intelligent Scene Modelling Information Systems, volume 181. Springer.
</a>

<a
  href="https://arxiv.org/abs/1703.00548"
  id="miikkulainen2019evolving">
Miikkulainen, R., Liang, J., Meyerson, E., Rawal, A., Fink, D., Francon, O., Raju, B., Shahrzad, H., Navruzyan, A., Duffy, N., et al. (2019). Evolving deep neural networks. In Artificial Intelligence in the Age of Neural Networks and Brain Computing, pages 293–312. Elsevier.
</a>

<a
  href="http://doi.org/10.1109/CCGRID.2018.00066"
  id="mollah2018comparative">
Mollah, M. A., Faizian, P., Rahman, M. S., Yuan, X., Pakin, S., and Lang, M. (2018). A comparative study of topology design approaches for hpc interconnects. In 2018 18th IEEE/ACM International Symposium on Cluster, Cloud and Grid Computing (CCGRID), pages 392–401. IEEE.
</a>

<a
  href="http://doi.org/10.1162/artl_a_00284"
  id="moreno2019toward">
Moreno, M. A. and Ofria, C. (2019). Toward open-ended fraternal transitions in individuality. Artificial life, 25(2):117–133.
</a>

<a
  href="http://doi.org/10.17605/OSF.IO/53VGH"
  id="Moreno_Ofria_2020">
Moreno, M. A. and Ofria, C. (2020). Practical steps toward indefinite scalability: In pursuit of robust computational substrates for open-ended evolution. DOI: 10.17605/OSF.IO/53VGH; URL: https://osf.io/53vgh.
</a>

<a
  href="https://doi.org/10.17605/OSF.IO/G58XK"
  id="dishtinygp">
Moreno, M. A. and Ofria, C. (in prep.). Spatial constraints and kin recognition can produce open-ended major evolutionary transitions in a digital evolution system.
https://doi.org/10.17605/OSF.IO/G58XK.
</a>

<a
  href="https://doi.org/10.1145/2739480.2754703"
  id="nguyen2015innovation">
Nguyen, A. M., Yosinski, J., and Clune, J. (2015). Innovation engines: Automated creativity and improved stochastic optimization via deep learning. In Proceedings of the 2015 Annual Conference on Genetic and Evolutionary Computation, pages 959–966.
</a>

<a
  href="http://doi.org/10.5281/zenodo.2575607"
  id="charles_ofria_2019_2575607">
Ofria, C., Dolson, E., Lalejini, A., Fenton, J., Moreno, M. A., Jorgensen, S., Miller, R., Stredwick, J., Zaman, L., Schossau, J., Gillespie, L., G, N. C., and Vostinar, A. (2019). Empirical. Packard, N., Bedau, M. A., Channon, A., Ikegami, T., Rasmussen, S., Stanley, K. O., and Taylor, T. (2019). An overview of open-ended evolution: Editorial introduction to the openended evolution ii special issue. Artificial life, 25(2):93–103.
</a>

<a
  href="http://dx.doi.org/10.7551/978-0-262-32621-6-ch128"
  id="soros2014identifying">
Soros, L. and Stanley, K. (2014). Identifying necessary conditions for open-ended evolution through the artificial life world of chromaria. In Artificial Life Conference Proceedings 14, pages 793–800. MIT Press.
</a>

<a
  href="https://www.oreilly.com/radar/open-endedness-the-last-grand-challenge-youve-never-heard-of/"
  id="stanley2017open">
Stanley, K. O., Lehman, J., and Soros, L. (2017). Open-endedness: The last grand challenge you’ve never heard of. O’Reilly Online.
</a>

<a
  href="http://doi.org/10.1162/106454603322221487"
  id="stanley2003taxonomy">
Stanley, K. O. and Miikkulainen, R. (2003). A taxonomy for artificial embryogeny. Artificial Life, 9(2):93–130.
</a>

<a
  href="http://www.gotw.ca/publications/concurrency-ddj.htm"
  id="sutter2005free">
Sutter, H. (2005). The free lunch is over: A fundamental turn toward concurrency in software. Dr. Dobb’s journal, 30(3):202–210.
</a>

<a
  href="https://doi.org/10.1038/30918"
  id="watts1998collective">
Watts, D. J. and Strogatz, S. H. (1998). Collective dynamics of ‘small-world’ networks. Nature, 393(6684):440.
</a>

## Acknowledgements

Thanks to members of the DEVOLAB, in particular Santiago Rodgriguez-Papa for help developing the DISHTINY web interface.
Thanks also to Ryan Moreno for feedback and suggestions on the asymptotic scaling proofs.
This research was supported in part by NSF grants DEB-1655715 and DBI-0939454, and by Michigan State University through the computational resources provided by the Institute for Cyber-Enabled Research.
This material is based upon work supported by the National Science Foundation Graduate Research Fellowship under Grant No. DGE-1424871.
Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation.
