---
layout: post
title: "But what IS a Timey McTimeface? And what does it do?"
date: 2021-06-26
no_toc: true
---

## What is?

![zoom screenshot showing timey mctimeface as a video guest](/resources/timey-mctimeface-screenshot.jpeg){:style="width: 100%;"}

Unfortunately, in Zoom land waving a "time's up" sign at presenters in meetings you're facilitating becomes much less effective --- and there's no room lights to flick if they try to cram in their remaining twenty slides anyways.

Timey McTimeface is a Zoom guest whose video camera shows a countdown timer that can help keep presenters on track.
Timey McTimeface can give an audio alert to presenters to let them know when they've got a certain amount of time left and beep incessantly at them when their time's up!

Because Timey works as a video feed rather than a screen share, they don't interfere with your presenters' slides!

## How to?

The trick behind Timey McTimeface is to convert an on-screen timer to a web feed.
[OBS Studio](https://obsproject.com/)'s "Virtual Camera" is a great choice for this.

You'll also need to redirect your computer sound to a virtual microphone.
Unfortunately, OBS Studio doesn't take care of this for you.
[PulseAudio Volume Control (pavucontrol)](https://freedesktop.org/software/pulseaudio/pavucontrol/) with a little [Stack Overflow magic](https://unix.stackexchange.com/a/584412) does the trick, though.

As for the actual on-screen timer, I've got a buggily-customized version I like that gives a configurable pre-expiration warning and indicates remaining time with background color available [here](http://mmore500.com/timeymctimeface/).
You can find plenty of other timers online.

Don't forget to set your favorite Dali painting as your clock guest's avatar!
Because your PC's zoom connection is busy wity Timey, you may have to join from another machine (maybe a phone).

## A Better Way?

Looks like there's also a proper [Zoom app](https://marketplace.zoom.us/apps/3Jdbzv64QnKYAT911tlV9Q) available for this same type of thing.
However, you need to have install permissions on your Zoom account to use it.

## Let's Chat

I would love to hear your favorite zoom tricks.

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">But what IS a Timey McTimeface? And what does it do???<br><br>new blog to answer these questions &amp; share a mini how-to on a neat trick to help keep your virtual presenters on track timewise ⏲️🤷<a href="https://t.co/tZrstfT54j">https://t.co/tZrstfT54j</a> <a href="https://t.co/JdHq1T7vgt">pic.twitter.com/JdHq1T7vgt</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1408981115935801344?ref_src=twsrc%5Etfw">June 27, 2021</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish: or make a comment :raising_hand_woman:
