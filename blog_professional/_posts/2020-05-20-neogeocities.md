---
layout: post
title:  "Neogeocities: Call for a Great GIF Restoration"
date:   2020-05-20
---

{% include gifscroll.html %}

<script>
GifDisable = function () {
  var allGifs = document.querySelectorAll('img[src$=".gif"]');
  for (gif of allGifs) {
    gif.src = "";
  }
  window.clearInterval(window.disableID);
}
</script>

*([Click here](javascript:GifDisable();) to strip animations from this page.)*

![A cool gif.](/resources/neogeocities-earth_mill.gif){:width="100%"}
*[source](https://web.archive.org/web/20091027020322im_/http://geocities.com/breakdancing2000/)*

In this erudite thinkpiece, originally prepared for a spoof presentation, I will
1. argue that GIFs today represent a mere shadow of GIFs of yesteryear,
2. propose a neogeocities renaissance for contemporary websites in which we extract the benefits of [geocities](https://en.wikipedia.org/wiki/Yahoo!_GeoCities)-style GIFs while avoiding the pitfall of sensory overload and distraction,
3. lay out a set of tools that make it possible.

This blog post isn't actually entirely ironic.
You can see a neogeocities site I put together [here](http://mmore500.com/waves/tutorials/lesson03.html).

Buckle up, buckaroos.

## GIFs Now: ephemeral

![A reaction gif.](/resources/neogeocities-giphy-cookiemonster.gif){:width="100%"}
*[source](https://giphy.com/gifs/office-working-DbV0RlRbSWYBG)*

Reaction GIFs enjoy a near-total hegemony over contemporary GIF usage.
We grab these gifs --- largely clipped from TV, film, or home video --- from a pop-up toolbar we searched "eyeroll" into, throw them into a twitter reply or facebook message, and forget about them.

These GIFs are a mere shadow of their forebearers...

## GIFs Then: handcrafted

![A very handcrafted gif.](/resources/neogeocities-dinosaurrocket.gif){:width="100%"}
*[source](https://web.archive.org/web/20091019112858/http://geocities.com/padinosaur/)*

GIFs used to be handcrafted.

Some of them, especially so.

Whether with low poly 3D rendering or Microsoft Paint, someone sat down to intentionally create a GIF.
GIFs weren't post-hoc scraps shed from another medium.

## GIFs Then: structural

![A title.](/resources/neogeocities-title.gif){:width="100%"}
*[source](https://web.archive.org/web/20090728194006/http://geocities.com/prezioso73/)*

GIFs used to play a structural role in web design.
They served as page headers, section breaks, menu items, and menu items.

{% include neogeocities-clock.html %}
*[source](https://web.archive.org/web/20090728100755/http://hk.geocities.com/katze_ting/)*

They even were used to display information in web apps.
In this example, a bona-fide JavaScript-powered clock.

## GIFs Then: collectible

{% include neogeocities-table.html %}
*[source](https://web.archive.org/web/20091027080309/http://hk.geocities.com/hehatogether/c1.htm)*

GIFs of old were collected, curated, cherished, and exchanged.
Maybe something like [pin trading](https://en.wikipedia.org/wiki/Pin_trading).
Geocities pages existed for the sole purpose of organizazing and proudly displaying GIFs.
GIFs constituted precious treasures, not throwaway commodities.

See also this [virtual stamp collection](http://geocities.com/angellovepsp/Stamp_Collection1.html) and this ["Free Mouse ,Hamster & more Blinkies and Gifs collection"](https://web.archive.org/web/20090829164804/http://geocities.com/victoriais2cute//index.htm)

## Toward Neogeocities: Finding Gifs

How can tap into the former glory of GIFs?
The first step is to find some glorious vintage GIFs.
Look no further than the [Internet Archive's](https://archive.org/) [GifCities](https://gifcities.org) project, a searchable collection of GeoCities GIFs.

Some tips:
* GIFs appear to be indexed based solely on filename and site name, so you might have to search a bit sideways to find what you're looking for.
* Steel yourself: there's no SFW filter... there are some truly fascinatingly horrible entries in there.
(I, for example, accidentally ran into Mr. Bean erotica.)

## Toward Neogeocities: Finite Looping

<marquee> Is this distracting? </marquee>

Yes, [yes it is](http://www.montulli.org/theoriginofthe%3Cblink%3Etag).

GIFs are fun, but when they keep on going and going and going they distractingly pry the eye away from most anything else visitors to a website are trying to digest.
(A loquatious thinkpiece with sophisticated vocabulary, for example.)

GIFs need not loop indefinitely, however.
You can actually specify a finite loop count, after which the GIF will halt.
If you let this rainbow GIF sit, for example, it'll freeze right up in a second or so.

![Rainbow.](/resources/neogeocities-rainbow.gif){:width="100%"}
*[source](https://web.archive.org/web/20021013045320/http://www.geocities.com/orcanut2002/)*

The [Gifsicle tool](https://www.lcdf.org/gifsicle/) makes setting loop count from the command line a snap.

```
gifsicle infinite.gif --loopcount=5 > finite.gif
```

or

```
gifsicle infinite.gif --no-loopcount > finite.gif
```

There are also plenty of [in-browser tools](https://ezgif.com/loop-count) that do the same.

## Toward Neogeocities: Restart on Scroll

Although we don't want GIFs GIF-ing all the time, we probably also don't just want them to once and done.
What about the juicy GIFs at the bottom of a page that would be all played out before web visitors get a chance to chance upon them?

I've found that re-triggering GIF animation on scroll provides a suitable solution.
GIFs can be their fun selves while you're navigating and moving, but once you actually want to focus in on something they tone right down.

![A title.](/resources/neogeocities-insanity.gif){:width="100%"}
*[source](https://web.archive.org/web/20091027012852/http://geocities.com/greekstyle121/)*

Here's the JavaScript that makes it work.
You can paste this right into a HTML file and be good to go!
(It's pasted in on this page!)

```
<script>
window.onscroll = function () {
  var allGifs = document.querySelectorAll('img[src$=".gif"]');
  for (gif of allGifs) {
    gif.src = gif.src;
  }
}
</script>
```

## Toward Neogeocities: Tiling Gifs

I find that GIFs make for super-cute section breaks in otherwise dry documents.
GIFs with a wide aspect ratio work best here.
You'll want to

[This web tool](https://ezgif.com/combine) makes horizontally tiling GIFs super easy.
(The UI doesn't work super great with wide images, but you can pop open your browser's web inspector and throw "style=width:2000px" into the GIF-staging table tag to crack it open if you run into issues).

## Toward Neogeocities: Accessibility

Animations can introduce accessibility issues for some of web visitors.
If you're using them ornamentally, it's a good idea to allow visitors to strip out animations if they need to.
Here's some HTML for a cute little button to do just that.

```
<script>
GifDisable = function () {
  var allGifs = document.querySelectorAll('img[src$=".gif"]');
  for (gif of allGifs) {
    gif.src = "";
  }
}
</script>

<a
  style="float: left; padding: 5px; position: relative;"
  href="javascript:GifDisable();"
  alt="Disable Animations"
>
  <span
    style="position:absolute; opacity: 0.2;"
  >
    :x:
  </span>
  <span
    style="opacity: 0.4; -webkit-filter: grayscale(1);"
  >
    :movie_camera:
  </span>
</a>
```

<blockquote>
  <a
    style="float: left; padding: 5px; position: relative;"
    href="javascript:GifDisable();"
    alt="Disable Animations"
  >
    <span
      style="position:absolute; opacity: 0.2;"
    >
      :x:
    </span>
    <span
      style="opacity: 0.4; -webkit-filter: grayscale(1);"
    >
      :movie_camera:
    </span>
  </a>
  <br/>
</blockquote>

## Neogeocities: A Prototype

Has all this piqued your interest?
Go give neogeocities a vibe check [here](http://mmore500.com/waves/tutorials/lesson03.html).
:sunglasses:

## Let's Chat!

What's your hot take on neogeocities?
What other aspects of the 90s internet should we revive?
Also, what is the adorable GIF subgenre of wholesome floating blob things called?
(I can't figure out how to Google them to find more!)

![what are these things called?](/resources/neogeocities-school.gif){:width="100%"}
*[source](https://web.archive.org/web/20090729063626/http://hk.geocities.com/polyuhditec/timetableYear2/timetable.html)*

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">blog post started out as a spoof presentation ...<br>... but also it&#39;s not entirely unironic<br><br>&lt;blink&gt;<br>✨Neogeocities: Call for a Great GIF Restoration✨<br>&lt;/blink&gt;<br><br>incl. some quality gifs &amp; some quality JS snippets :🤷<a href="https://t.co/yZnUkTnmqD">https://t.co/yZnUkTnmqD</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1263574874347323393?ref_src=twsrc%5Etfw">May 21, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
