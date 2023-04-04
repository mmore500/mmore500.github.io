---
layout: post
title: "Hard-won Research Workflow Tips"
date: 2022-12-04
no_toc: true
hidden: true
---

## Number Seeds Starting at 1,000

Ensures alphabetical ordering of string representation matches numerical ordering.
This tip credit [@voidptr](https://github.com/voidptr)

## Have low-numbered seeds run quick, pro-forma versions of your workflow

Good for debugging.
Your workflow won't work the first or second time.
The first time you run your workflow is NEVER to generate actual data.
It is to debug the workflow.

Spot check all data files manually.

## Divide seeds into completely-independent "endeavors"

No data collation between endeavors.
Allows completely independent instantiations of the same workflow.

## Do you have all the data columns you'll want to join on?

if you gzip, redundant or always-same columns shouldn't take up much extra space

## How will you manually re-start or intervene in the middle of your workflow when things go wrong?

## How will you weed out bad or corrupted data from good data?

Ideally, different runs will be completely isolated so this is not necessary

## How will you play detective when you find something weird?

## Use JSON, YAML, etc.

don't invent your own serialization format

## Save SLURM job ID and hard-pin job ID with *all* data

## Save SLURM logs to one folder, named with the JOB ID

Consider using symlinks

## Also save a copy of SLURM scripts to a separate folder, named with the JOB ID

This makes it easy to debug, rerun, or make small manual changes and rerun.

## A 1% or 0.1% failure rate == major headache at scale

Request *very* generous extra time on jobs or, better yet, use time-aware experimental conditions (i.e., run for 3 hours instead of n updates)

## Use Jinja to instantiate batches of job scripts

## Hard-pin your source as a Jinja variable

Subsequent jobs should inherit parent's hard pin

## Embed large numbers of jobs into a script as a text variable representation of `.tar.gz` data

<https://github.com/mmore500/dishtiny/blob/bdac574424570fb7dc85ef01ba97464c6a8737cc/script/slurm_stoker_kickoff.sh>

<https://github.com/mmore500/dishtiny/blob/bdac574424570fb7dc85ef01ba97464c6a8737cc/script/slurm_stoker.slurm.sh.jinja>

## Re-clone and re-compile source for every job

Use automatic caching instead of manual caching
* `ccache`
* <https://github.com/mmore500/dishtiny/blob/bdac574424570fb7dc85ef01ba97464c6a8737cc/script/gitget.sh>

## Get push notifications of job failures

Automatically upload to logs to `transfer.sh` to be able to view as embedded link

Running experiments equals pager duty.

## Get push notifications of your running job count

## Have every job check file quota on startup and send push warning if quota is nearing capacity

<https://github.com/mmore500/dishtiny/blob/bdac574424570fb7dc85ef01ba97464c6a8737cc/script/check_quota.sh>

## Have all failed jobs try rerunning themselves once

## If it happens once (i.e., not in a loop), log it

## Log full configuration and save an `asconfigured.cfg` file

## Log ALL Bash variables

## Log RNG state

## Timestamp log entries

## Put everything that might fail (i.e., downloads) in an automatic retry loop

## Log digests and row count of all data read in from file

in notebooks and in simulation

## gzip log files and save them, named by SLURM job ID

Your data has SLURM job id, so it is easy to find relevant log when questions come up

## You can open URLs directly inside `pandas.read_csv()`

i.e., OSF urls

## You can open `.csv.gz`, `.csv.xz` directly inside `pandas.read_csv()`

Consider using a library to save to `gz` filehandle directly.

## Notebooks

* commit bare notebooks
  * consider adding a git commit hook or CI script to enforce this
* run notebooks inside GitHub actions
  * consistent, known environment
  * enforces EVERY asset MUST be committed or downloaded from URL
  * keeps generated cruft off of main branch history
  * use `teeplot` to generate and save copies of all plots with descriptive, systematic filenames
  * github actions pushes new executed notebooks, generated assets to a `binder` or `notebooks` branch
  * be sure to push so that history on that branch is preserved
* include graphics in LaTeX source as git submodule
  * get new versions of graphics as `git pull`
  * be sure to use `--recursive --depth=1 --jobs=n` while cloning

## Overleaf doesn't like git submodules

AWS Cloud9 is a passable alternative, but it's hard to get collaborator buy-in and annoying to manage logins and permissions

## Use symlinks to access your in-repository Python library

## Create supplementary materials as a LaTeX appendix to your paper

Makes moving content in/out of supplement trivial.
You can use `pdftk dump_data_utf8` to automatically split the supplement off into a separate document as the last step of the build.

## Everything MUST print a stack trace WHEN it crashes

<https://github.com/bombela/backward-cpp>

Consider adding similar features to your job script with a bash error trap
<https://unix.stackexchange.com/a/504829>

## Be sure to log node name on crash

Some nodes are bad.
You can exclude them from letting your jobs run on them.

## Use `bump2version` to release software

<https://github.com/c4urself/bump2version>

## Use `pip-tools` to ensure a consistent Python environment

<https://pypi.org/project/pip-tools/>

## Don't upload to the OSF directly from HPCC jobs

Their service isn't robust enough and you'll cause them issues.
AWS S3 is an easy alternative that integrates well.

## Make it clear what can be deleted or just delete immediately

Otherwise you will end up with a bunch of stuff and not remember what's important

Put things in `/tmp` so they're deleted automatically.

## ondemand

<https://ondemand.hpcc.msu.edu/>

Great for browsing, downloading files.
Also for viewing queue and canceling individual jobs.
