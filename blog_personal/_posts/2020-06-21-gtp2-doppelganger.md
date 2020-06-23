---
layout: post
title: "not now sweetey, mommy's making gpt2 performance art on twitter"
date: 2020-06-21
---

*All fun shenanigans described here were undertaken in a purely personal capacity.*
*This endeavor is **not** a professional activity associated with my role in any lab/institution or any funding/support I receive.*

As you do from time to time, I recently stumbled upon an anonymous, and often political, twitter asshole.
This persona was preoccupied generating 100% USDA certified tool content, but (much to my own chagrin, as pretentious a prick as he was) I had to admit somewhat admired his wit.

To protect the anonymity of everyone involved, I've decided against embedding any material here or linking back.
(But if I know you & you're curious, DM me.)

I ruminated on the best way to:
1. tell this guy off for being a tool while
2. not being a tool myself and
3. denying him the satisfaction of a last word.

![A quality meme](/resources/gtp2-doppelganger-meme.jpg){:width="100%"}

I figured it had to be something entertaining and strange.
Why not point out how self-involved & disconnected from reality his account was by using machine learning to impersonate him?
Sounded like a fun weekend to me.

## Scrape Some Data

The first step, or course, was scraping [@Mottl](https://github.com/Mottl)'s [GetOldTweets3](https://github.com/Mottl/GetOldTweets3) tool made this pretty easy --- no API key required.

Then I just ran a quick python script to make a training data set out of the scraped data.

```python
import pandas as pd

df = pd.read_csv("output_got.csv")
with open('training_data.txt', 'w') as f:
  for tweet in df["text"].dropna():
    f.write(str(tweet))
    f.write("\n==========\n")
```

## Bake that Sucker

Pop a model in the oven using some nice [copy-paste code from Medium](https://towardsdatascience.com/how-to-make-a-gpt2-twitter-bot-8669df60e60a).

If you don't have your own GPU sitting around, you can [rent GPU time](https://blog.thedataincubator.com/2018/04/gpu-cloud-computing-compared/) for not too much nowadays.

## Rough Diamonds

This might not be as funny without being familiar with the source account, but `¯\_(ツ)_/¯`.

> The grievance theory has several dimensions: 1) it invalidates my claim that the grievance theory is invalid 2) it invalidates my claim that grievance theory evidence is motivated by grievance grievance 2) it invalidates my claim that grievance theory reasoning is motivated by grievance grievance 3) it invalidates my claim that grievance theory evidence is motivated by grievance grievance 2) it invalidates my claim that grievance theory reasoning is motivated by grievance grievance

> The brain is a complex web of interconnected neurons. Your social standing, your academic standing, your academic status, is all tied to the ensemble of neurons around you. For example, the right ventrolateral prefrontal cortex (VMPFC) is connected to the nucleus of the stria terminalis (NST).

> The man with the beard: "I'm going to be the man whose life I will lead" and "I want to be seen as a hero"

> It's ok to invade countries that have banned guns.

> Harry Potter and the Half-Woman Princes

> My dad was concerned that my dadma would be upset if I did not tell him what to do when he gets the wrong answer.

> Positivism is when you agree with everything I say.

> This reminds me of when I said "The Simpsons is canceled because of this."

> This could be explained by foresight.

> I've always been a fan of women's underwear, and I admire their bravery in the face of oppression.

> The women's network of insula (the one responsible for sympathy) and hypothalamic (the one responsible for vengeance) remain the same.

> I don't know what the heck is wrong with me, but I do know that I am pretty screwed up emotionally.

> Every time you throw out "socialism" you make the opposite statement.

> NLP is when you say "no" while avoiding a question mark.

> I don't know what the heck is wrong with me, but I do know that I am pretty screwed up emotionally.

> White people resent being called "racist"

> I'm going to burn down your house to make room for Barbie

> The idea that women can't get laid is true for all religions.

## Window Dressing

Scraping down the target's profile picture your browser's developer view.
(Usually `ctrl-shift-i`.)
Load up their profile and monitor images that are loaded up in the Network view.

[Google voice](https://voice.google.com/) is a good way to get a semi-anonymous phone number to set up a semi-anonymous parody account.
(You can get doxed by the four or so digits of the phone number that are displayed on the password reset button.)

## An Art

My initial take was to generate a bunch of tweets and schedule them to post on the parody account.
This was fun for a while.

Then I played around with joining in on twitter conversations the target account had been involved in, but this got me blocked.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">.<a href="https://twitter.com/msubroad?ref_src=twsrc%5Etfw">@msubroad</a> please make my week &amp; hang a bathroom stall door in your gallery space <a href="https://t.co/gTYl8INEC8">https://t.co/gTYl8INEC8</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1224068365729157120?ref_src=twsrc%5Etfw">February 2, 2020</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Who would have guessed that my initial, finely-tuned artistic instincts could have been too aggressive.

## Retweet

I regrouped and settled on a doppelganger format where I retweet the target adding a generated comment seeded on the first few words of the original tweet.
I made a second account to try this out and, so far, at least haven't got blocked yet.

Here's an example of what this looks like, with a bot trained on Drumpf.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I gave John Bolton, who was incapable of being Senate confirmed because of his stupid line of reasoning, a little more money to help him win the White House. This is a disaster for American families! <a href="https://t.co/XktWcStgOu">https://t.co/XktWcStgOu</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1275245909761069057?ref_src=twsrc%5Etfw">June 23, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

This could format could be adjusted to be slightly more invasive by commenting on the original tweets.

## Keeping up with the Kardiashians

The ideal way to set up this type of system would be as a completely autonomous bot.

However, while I've been playing around with the concept I've just been running the parody account manually.
[Zapier](https://zapier.com/)'s tweet to email service provides a nice, discreet way to keep up with the target's tweets.
I think you could also set up twitter to notify you whenever someone specific you're following tweets.

## But is it Ethical?

Probably not `¯\_(ツ)_/¯`.
I guess my real question is, how unethical is it?

Some questions for small-group discussion:
* At what point is this just harassment?
* If you're mimicking a horrible account, at which point are you just tweeting more horrible things.
* By following the parody account are you just setting yourself up to be Stockholm syndrome-d to all the horrible things.

## Future Work if I Feel Like It

![A quality certificate](/resources/gtp2-doppelganger-certificate.jpg){:width="100%"}

With my glorious Certificate of Twitter Achievement in hand from [@leg2015](https://twitter.com/leg2015), the future is a bright vista spread before me!
At least while I play around with this project for another week and then forget about it.

Until then, here's what I'm thinking about:
* automation
  * how to automatically select seed text?
  * how to automatically select generated text among alternate options to maximize entertainment value?
  * how to automatically screen out truly horrible, unconscionable things from generated text?
    (I've already had to do this a few times manually.)
* better model
  * especially RE: working with seed text, where gpt-2 doesn't seem to fare particularly well
  * how much to train the model and what "temperature" (zaniness) parameter settigns to use
    * if the model mimics the target without being slightly absurd, it's not too entertaining
* bigger, more public target
  * probably someone political with a distinctive twitter personality would be a good choice

## Let's Chat!

What future directions should I take this project in?
What tools or techniques should I consider using?
What is *your* critical interpretation of this piece?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">posted a new blog,<br><br>&quot;not now sweetey, mommy&#39;s making gpt2 performance art on twitter&quot;<a href="https://t.co/FAhpmLENKj">https://t.co/FAhpmLENKj</a><br><br>enjoy!! ✨<br><br>DM me for deets if you&#39;re curious and would like to take a peek at the ongoing dumpster fire 😉</p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1275274264375996417?ref_src=twsrc%5Etfw">June 23, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
