---
layout: post
title:  "Gotta Go Fast: Quick & Dirty Shell Edition"
date:   2019-11-16
no_toc: true
---

> I want to do the same thing to a whole ton of different data files or whatever.
> It's not, like, a super hard thing.
> It takes like a minute or ten minutes
> In fact, if it were one data file I'd just get the thing going, grab a chocolate milk from the third-floor vending machine, & then get on with my dab.
>
> But it's not just one data file.
> It's never just one data file.
> It's threeve-bazillion of them.
>
> I could make the thing go one at a time, but then I'd have to figure out something else to start doing while the things do the thing one thing at a time.
> I just want to do the thing I'm doing instead.
>
> --- you, probably

Hi, I'm an impatient graduate student with the attention span of a goldfish and the multitasking capacity of a golden retriever who is also chewing gum.
And I want to tell you: there IS hope.
We CAN do the thing on the different things all at the same time on our SLURM-based compute cluster.
And it's not even that hard.

## Example Thing

Let's get our Cruell-tar De Vil on.

This shell command

```bash
for i in {1..101}; do echo "a good use of cluster time" > "doggo-$i.data"; done
```

creates a data file for each of our 101 and one dalmatians.

```
doggo-100.data
doggo-101.data
doggo-10.data
doggo-11.data
doggo-12.data
doggo-13.data
doggo-14.data
doggo-15.data
doggo-16.data
doggo-17.data
doggo-18.data
doggo-19.data
doggo-1.data
doggo-20.data
doggo-21.data
...
```

Dalmatians are more lucrative when they are small (for... wholesome, non-fur coat reasons), so we want to use `tar` to zip up our data.
Here's what zipping up one data file looks like.

```
tar -czvf doggo-1.data.tar.gz doggo-101.data
```

But we want to do this to *all* 101 of our dalmations.

## Serial-ously Lame Plain Bash Loop

We could use a bash for loop (over `*.data`) to zip up each data file one at a time...

```bash
for f in *.data; do tar -czf $f.tar.gz $f; done
```

## Bash Loop With Backgrounding For Great Good

... *or* we could fork off each piece of the inner loop (by appending an `&` to the inside bit) as soon as we hit it, so all the data files get processed simultaneously.

```bash
for f in *.data; do tar -czf $f.tar.gz $f &; done
```

This works great until the number of work items begins to outstrip the available compute cores.
If you're working on a shared dev node, it's probably not polite to hog up all the cores for more than maybe a few minutes or so.
Use `salloc` to request an interactive job where you'll have the compute resources all to yourself, and you won't be bothering anybody else.
Here we're asking for 24 cores `-n 24` on one node `-N 1`.

```bash
salloc -N 1 -n 24 --time=3:00:00
```

Two important points here:
1. Don't request more cores on one node than are available on any node because then your job will never schedule.
Consult [your local cluster's documentation](https://wiki.hpcc.msu.edu/pages/viewpage.action?pageId=20120131) for information on available hardware configurations.
Also, you'll probably have to wait a whole long time to get a node all to yourself, so consider requesting fewer cores so your interactive job schedules faster.
2. Don't request more than one node because your shell can only use the resources from one node.
(You need MPI or other fancy pants tools to distribute computations over multiple nodes).

But what if we want to do MOAR things at once then is reasonable on a single node?

## Bash Loop With `srun` For Greater Good

Enter `srun`, which will schedule a lil' SLURM job for you.
Tell it how many minutes the job will last (e.g., `-t 20`) and then what you want it to do right after that.

```bash
for f in *.data; do srun -t 20 bash -c "cd ${PWD} && tar -czvf ${f}.tar.gz ${f}" &; done
```

Note that `srun` blocks until the requested job is complete, so we just fork off in to the backround all our `srun`s with an `&` at the end of the inside bit.
We slapped `"` marks around the work part so that our intended command would get forwarded correctly to `srun` (i.e., the `&&` wouldn't be applied during the call *to* `srun` a la `srun && tar`).
Also, `srun` doesn't execute your command in a full-fledged shell, so we have to have to ask `srun` to start `bash` to execute our command (provided after the `-c` argument).
Inside the command, we have to start by `cd`ing to our current working directory because the SLURM job won't necessarily start there.

## Bonus Round: Get A `grep` On The Cluster Gremlin

Intermittent failures, especially when you start using `srun`, are inevitable.
Thank you, cluster gremlin.

So, we're going to want to quickly re-do the bits that failed.
Let's wrap the `srun` do-work part in an if statement that checks --- for each work item --- whether the relevant output file exists.
If the relevant output file DOES exist, then skip the request to `srun` with that output's work item.

```bash
for f in *.data; do if ! ls *.tar.gz | grep -q $f; then srun -t 20 bash -c "cd ${PWD} && tar -czvf ${f}.tar.gz ${f}" &; fi; done
```

We use `grep -q` to [`grep` quietly](https://www.tiktok.com/@mandymathews8/video/6754593887798529286) so that we only see the exit status (i.e., did it successfully find a match) and don't get distracting tidbits printed out to the screen.

You can pipe `ls` into `wc -l` (word count lines) to make sure all the work items were successfully completed by comparing the count of work items to the count of outputs.

```bash
ls *.data | wc -l
ls *.data.tar.gz | wc -l
```

If your parallelized work item doesn't generate a file output on success (or one that's easy to relate back to the original file name), you can conditionally append the name of each operand file to a log file (here, `log.log`) on successful completion of the work item by chaining another command on with `&&`.

```bash
for f in *.data; do srun -t 20 bash -c "cd ${PWD} && tar -czvf ${f}.tar.gz ${f} && echo ${f} >> log.log" &; done
```

Then, to round up the stragglers, we `grep` through the log file for the source file of the work item under consideration.

```bash
for f in *.data; do if ! cat log.log | grep -q $f; then srun -t 20 bash -c "cd ${PWD} && tar -czvf ${f}.tar.gz ${f} && echo ${f} >> log.log" &; fi; done
```

Working with a log file like this, you can `cat` the log file to count the number of *successful* work items.

```bash
cat log.log | wc -l
```

## Let's Chat

I would love to hear your thoughts, questions, and comments RE: SLURM shell kung fu!!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">fresh on the good ol&#39; blog: some tips for parallel shell-fu on your local SLURM cluster <a href="https://t.co/gvM1VtWJQQ">https://t.co/gvM1VtWJQQ</a><br><br>🤬 ⏩ 🥰<br>(results may vary)</p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1195607006423371777?ref_src=twsrc%5Etfw">November 16, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
Pop on there and drop me a line :fishing_pole_and_fish:, make a comment :raising_hand_woman:, or leave your own tips & tricks :heart:
