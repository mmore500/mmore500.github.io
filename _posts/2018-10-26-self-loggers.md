---
layout: post
title:  "Setting Up Self-Loggers"
date:   2018-10-26
---

A few weeks ago, I passed my comprehensive exam.
I finish up my coursework this spring.
So, I've been in the mood to look forward.
Looking forward, of course, means looking towards the dissertation.

On average, [1.6 people read a PhD thesis all the way through --- including the author](https://www.nature.com/news/the-past-present-and-future-of-the-phd-thesis-1.20207).
In most cases, the thesis does *not* function as a vessel for scientific knowledge.
At risk of stating the obvious: more than anything else, the thesis exists as an artifact of graduate education.
The function of the thesis, its raison d'être, is [personal and professional growth.](
https://www.nature.com/news/back-to-the-thesis-1.20202)
Put another way, the utility of the thesis stems from the process of document preparation rather than the prepared document.

When I finish up my dissertation, I'd like to be able to tell a neat story about the process of putting it together.
I hope that documenting and sharing my own experience might help make graduate school less mysterious and more approachable, particularly for underrepresented students.
Plus, I hope *anticipating* performing a reflection on my own challenges and growth --- through the magic of [preemptive retrospection](https://scholarsarchive.byu.edu/etd/1688) --- will help me experience [the latter "joys"](http://phdcomics.com/comics/archive.php?comicid=1420) of graduate school as patiently and positively as possible.

I'm a big believer in the utility of [narrative reflection](http://devosoft.org/reflections-on-my-first-semester-at-macdonald-middle-school/).
(Shout-out to [the CWLT](https://pugetsound.edu/cwlt)!)
Sitting down to write a paragraph about pretty much anything can make you discover *something* meaningful about it you didn't know before.
Usually, I start hacking out a reflection like "Sure... that's bit of a reach... whatever" but then this weird thing happens where, a few minutes or months later, I actually believe whatever I came up with.

I anticipate that baking data into a narrative reflection will yield an even more compelling story, lending engaging detail and perhaps even pointing my thinking in directions I wouldn't have considered otherwise.
I'm inspired by the stories [Kazuo Yano](http://gecco-2018.sigevo.org/index.html/tiki-index.php?page=Keynotes) and [Steven Wolfram](https://www.glassdoor.com/Reviews/Wolfram-Research-Reviews-E14501.htm) have told, respectively, via nifty [wrist-accelerometer data](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.497.4009) and  [phone/email/keylogger/more data](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/).
Cute statistics and nifty visualizations make good buzz marketing fodder on academic twitter, too. :wink:

Of course, in order to live out my dream, I've gotta set myself up with data to play with when the time arrives!

## Key Logger

I chose to use [logkeys](https://github.com/kernc/logkeys).
Although [their README](https://github.com/kernc/logkeys/blob/master/README.md) very modestly plugs other Linux key logging software, a few minutes' worth of poking around on Google revealed it to be the only reasonably maintained option.

I also considered [SelfSpy](https://github.com/selfspy/selfspy), which is a bit more than just a keylogger.
SelfSpy also tracks mouse movement and which window you have in focus.
SelfSpy is in particular distinguished by the well-developed suite of analysis tools packaged with it that work seamlessly.
To my (very cursory) judgment, the amount of recent development/maintenance activity underwhelms its heavy footprint.
I figured I'd have a better chance of collecting a continuous stream of data (or, realistically, more useful bits of patchy data) over the time-frame from here to graduation with logkeys.
Plus, I had a bad time trying to get SelfSpy going as a background process and gave up.

### Logkeys with Multiple Keyboards

Of course, setting up logkeys required clearing an annoying set of hurdles.

I use an [external keyboard](https://ergodox-ez.com/) when I work at my desk.
If your go-to machine is a laptop you never use an external keyboard with or a desktop computer with just one keyboard, you can install logkeys as usual (e.g., perhaps `sudo apt-get install logkeys`) and skip this subsection.
Otherwise, read on.

Luckily for us, [bryan-hoyle](https://github.com/bryan-hoyle) already did the heavy lifting.
He wrote [a patch for logkeys](https://github.com/kernc/logkeys/tree/bace087155e7c54293d44341fa552fb229d588ac) that allows logkeys to multiplex input from several keyboards.
Unfortunately, as of October 2018, [his pull request](https://github.com/kernc/logkeys/pull/171) to bring the fixes into `master` has been gathering dust for a full year.
So, you'll need to install logkeys from the tip of his development branch instead of `master`.

~~~
git clone https://github.com/kernc/logkeys
cd logkeys
git reset --hard bace087155e7c54293d44341fa552fb229d588ac
./autogen.sh     # generate files for build
cd build         # keeps the root and src dirs clean
../configure
make
sudo make install
~~~

See the [logkeys `INSTALL` documentation](https://github.com/kernc/logkeys/blob/master/INSTALL) for details/prerequisites.

As inevitable in [software install sagas](https://xkcd.com/1742/), another misfortune befalls us: logkeys keyboard multiplexing seems to require availability of all the keyboards you want to to capture from at logkeys startup.
That means, when we plug in or unplug an external keyboard, we need to re-launch `logkeys` in order to ensure correct logging.
(Otherwise, logkeys will completely ignore input from an external keyboard in the first case and incorrectly double-enter input from remaining keyboard in the other case).

Ideally, we'd just hook logkeys restarts into keyboard plug-in/unplug events via `/etc/udev/rules.d/`.
Unfortunately, I found that hooking logkeys launch into keyboard plug-in events somehow interfered with keyboard set-up, making the external keyboard not work at all.
I have no idea why.

After an hour or two of whack-a-mole trial and error, I settled on a workable (although not totally idea) solution:
1. having a keyboard connect/disconnect event kill the currently running logkeys process
2. using crontab to *attempt* logkeys launch every few seconds (if logkeys is currently running, no action is taken)

To accomplish part 1 of the solution, I created a new file, `/etc/udev/rules.d/100-mount-ergodox.rules`, containing the following rules

~~~
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="feed", ATTRS{idProduct}=="1307", RUN+="/usr/local/bin/logkeys -k"
ACTION=="remove", SUBSYSTEM=="usb",  RUN+="/usr/local/bin/logkeys -k"
~~~

You can replace `ergodox` in the filename with a slug referring to your keyboard.
In this snippet, `feed` and `1307` are the hex codes specifying my external keyboard's vendor and model.
To get your keyboard's vendor and model, run `lsusb` with your external keyboard unplugged,

~~~
lsusb
~~~

yielding

~~~
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 138a:0097 Validity Sensors, Inc.
Bus 001 Device 004: ID 04f2:b5ce Chicony Electronics Co., Ltd
Bus 001 Device 003: ID 8087:0a2b Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
~~~

then plug in your external keyboard and run `lsusb` again.

~~~
$ lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 138a:0097 Validity Sensors, Inc.
Bus 001 Device 004: ID 04f2:b5ce Chicony Electronics Co., Ltd
Bus 001 Device 003: ID 8087:0a2b Intel Corp.
Bus 001 Device 010: ID feed:1307
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
~~~

The entry that appeared on the second run of `lsusb` contains the hex codes specifying your keyboard's vendor and model.

Once you have the new rules in place, you'll need to register them.
If you don't want to reboot, you'll need to reload the `udev` rules to get your hooks running.

~~~
udevadm control --reload-rules && udevadm trigger
~~~

In order to accomplish part 2 of the solution, I put the following script in place at `/etc/init.d/logkeys-start.sh`

~~~
#!/bin/bash
### BEGIN INIT INFO
# Provides:          logkeys-start
# Required-Start:    $all
# Required-Stop:
# Default-Start:     2 3 4 5
# Default-Stop:
# Short-Description: Starts logkeys...
### END INIT INFO

/usr/local/bin/logkeys -s -m /home/mmore500/.config/logkeys/mylang.map
~~~

By placing this script in `/etc/init.d/`, logkeys will be launched on boot.
I discovered that the commented header was necessary to register the script for launch on boot.

Here, `-m /home/mmore500/.config/logkeys/mylang.map` provides a custom keymap for logkeys.
[See below](#logkeys-keymap) for details on testing whether you need a custom keymap and setting one up.
If you don't need to make a custom keymap, you can omit `-m /home/mmore500/.config/logkeys/mylang.map`.
Otherwise, you'll need to switch out `/home/mmore500/.config/logkeys/mylang.map` with whatever path you put your custom keymap on.

I call the `logkeys-start.sh` script via crontab every five seconds.
This way, logkeys will promptly resurrect after keyboard plug-in/unplug events kill it.
When logkeys is running, calling `logkeys -s` has no effect.

Here's the relevant addition to my `/etc/crontab`.
~~~
* * * * * root /etc/init.d/logkeys-start.sh
* * * * * root sleep 5; /etc/init.d/logkeys-start.sh
* * * * * root sleep 10; /etc/init.d/logkeys-start.sh
* * * * * root sleep 15; /etc/init.d/logkeys-start.sh
* * * * * root sleep 20; /etc/init.d/logkeys-start.sh
* * * * * root sleep 25; /etc/init.d/logkeys-start.sh
* * * * * root sleep 30; /etc/init.d/logkeys-start.sh
* * * * * root sleep 35; /etc/init.d/logkeys-start.sh
* * * * * root sleep 40; /etc/init.d/logkeys-start.sh
* * * * * root sleep 45; /etc/init.d/logkeys-start.sh
* * * * * root sleep 50; /etc/init.d/logkeys-start.sh
* * * * * root sleep 55; /etc/init.d/logkeys-start.sh
~~~

### Logkeys Keymap

I run [elemenary OS](https://elementary.io/) on a [Lenovo Thinkpad Carbon](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/ThinkPad-X1-Carbon-5th-Gen/p/22TP2TXX15G).
In order to get correct key log output, I had to define a custom keymap.

If you're lucky, you might not have to worry about this detail, either!
Try this to check if you might need a custom keymap.
Start logkeys up with the default keymap.
~~~
logkeys -s
~~~

Now, peek into the key log.
~~~
sudo tail /var/log/logkeys.log --follow
~~~

Then, systematically push every single button on your keyboard keep an eye on the key log.
Does what's showing up in the log match what you're pressing?
If so, great.
If not, you'll need to create a custom keymap.
~~~
sudo logkeys --export-keymap=mylang.map
~~~

Are `y` and `Y` appearing where `u` and `U` should?
Open up the keymap with your favorite editor.
Go find the line that reads `y Y` and make it read `u U` instead.

Restart logkeys with the custom keymap to try it out.
~~~
sudo logkeys -k
sudo logkeys -s -m mylang.map
~~~

As before, check if, using the custom keymap, what shows up in the log matches what you're pressing.
Continue to make changes as needed, restarting logkeys each time.

Here's what my keymap ended up looking like.

<script src="https://gist.github.com/mmore500/1dcfc0813c88b5e383f9bbb72914e918.js"></script>

I arbitrarily keep it at `~/.config/logkeys/mylang.map`.

For more details on the inner workings of the logkeys keymap, [see here](https://github.com/kernc/logkeys/blob/master/docs/Keymaps.md).

### Security

If you set up a keylogger on your computer, that means... you're running a keylogger on your computer, yo.
All of your passwords and [your dirty, dirty secrets](https://andburch.github.io/selfspy/) are recorded in a file someone else might be able to get their hands on.
If you work with sensitive information, there are probably rules you might want to make sure you're not breaking.

On the flip side of the coin, recording everything you ever type might be useful for recovering lost work in the event of a deletion disaster.
(Probably would require the application of some elbow grease, but still.)

## Keyboard Connect/Disconnect Logger

Hooking into keyboard connect/disconnect events to make `logkeys` work, I realized that they keyboard connect/disconnect events might tell an interesting story in and of themselves.
If my keyboard is plugged in, that's a pretty good sign I'm working at my desk.
Otherwise, I'm probably enjoying a bespoke espresso at my favorite upscale coffee shop.
(Hahahahaha, no, I'm working in bed.)

I threw together two very rudimentary scripts, which record timestamps of plug-in/unplug events in separate log files.

Here's `/usr/bin/log-plugin.sh`.

<script src="https://gist.github.com/mmore500/c555c8a1be00a95aedfda128554fc902.js"></script>

Here's `/usr/bin/log-plugout.sh`.

<script src="https://gist.github.com/mmore500/c9699887a1da7ac9d40bb9e7987746ae.js"></script>

To trigger these scripts on plug-in/unplug events, I added the following two rules to my `/etc/udev/rules.d/100-mount-ergodox.rules`.
~~~
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="feed", ATTRS{idProduct}=="1307", RUN+="/usr/bin/log-plugin.sh"
ACTION=="remove", SUBSYSTEM=="usb",  RUN+="/usr/bin/log-plugout.sh"
~~~

Ideally, the remove rule would be specific to *just* my keyboard.
It isn't.
`log-plugout.sh` runs every time I unplug any usb device.
That's why I threw the output of `lsusb` into `log-plugout.sh`.

Again, you'll need to reboot or reload the `udev` rules to get these hooks running.
~~~
udevadm control --reload-rules && udevadm trigger
~~~

## Wi-Fi Logger

I have two desks --- one at work and one at home.
I realized I might want to be able to distinguish which desk I'm working at.
The answer to recognizing which desk I'm at: which Wi-Fi signal I'm on.
Which Wi-Fi should tell other interesting stories, too, like how much work I do on- versus off-campus.

Here's the script.

<script src="https://gist.github.com/mmore500/a4c4d0dae5cae303d9006bbf2fab538d.js"></script>

Apparently, it's important for this one to not end in `.sh`.

## Document Logger

In what order over time did a document/codebase come together?

![](http://blog.stephenwolfram.com/data/uploads/2012/03/NKSBookMods-1991r.png){:width="100%"}

*Work on the different sections of Steven Wolfram's* A New Kind of Science *leading up to publication.*
[[Source]](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/)

If you use a version control system like [git](https://git-scm.com/), you should already be collecting the information you need to answer a question like this!
5
Your commit history can tell a story about yourself, too, not just your projects.
GitHub already stitches together your commit pattern across projects to make neat annual visualizations.

![](https://osf.io/4dn2q/download){:width="100%"}

I can see time off for winter break and a few deadlines on this one from 2018.
In contrast, my advisor maintains a [very impressive (terrifying?) 365/365 record](https://github.com/mercere99)
You can find yours on your Github profile.

## Calendar

If you use an electronic calendar, you've probably got a solid record of your scheduled events --- the [weightlifting sessions with Squee](https://www.youtube.com/watch?v=VRJecfRxbr8), and everything else --- going back a few years... unless you switched providers.
I'm looking forward to visualizing how the fraction of my days that are scheduled changes over time.

## Photos

At least to me, the [archive view of my photo tumblr](http://mmore500.tumblr.com/archive) is very descriptive of where I've been and what I've been up to over the past few years.

The content of the photos themselves tells the richest story, but I think that there might be other interesting threads to pull out of my RAW metadata.
What times of day or weeks of the month do I tend to shoot during?
How has the total shutter count of my camera progressed relative to the number of photos I've chosen to keep?
I [cull and archive my RAW files](https://mmore500.github.io/2018/01/22/my-photography-workflow.html) on a monthly basis, so I should be setting myself up with the data I need if I ever decide to play with those analyses.

## Fitness Trackers

I use a [Garmin Vivosmart 3](https://www.amazon.com/gp/product/B07BH3XN3T/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1), which was cheap has a decent sensor suite.
My wristband has a heart rate sensor, accelerometer, and altimeter.
There's no GPS, which is fine by me for the longer battery life.

The major point I was dis-satisfied about from all wearable device trackers is data availability.
If I can't open the data myself in Pandas, does it really matter that it exists?
I originally got a Garmin device because it looked like I would have the best chance of being able to scoop the raw data files of the device myself and bypass the (ubiquitously opaque) cloud services wearable vendors provide.

Thanks to [GDPR](https://forums.garmin.com/forum/into-sports/garmin-connect/feature-requests/1343456-download-of-all-health-data-as-required-under-gdpr), it looks like there's an better option: let Garmin perform automatic syncs and store the raw data files in its cloud, then pull the raw data down in full when I'm ready to play with it.
Maybe being [spammed for months on end](https://xkcd.com/1998/) earlier this year was worth something, after all!

The Garmin GDPR complance isn't actually baked into their [main interface](https://connect.garmin.com/modern/).
You find it through their ["account manager"](https://www.garmin.com/en-US/account/profile/).
You have to request a data export and then wait while they prepare it.
Garmin claims you should expect to wait two days (and perhaps up to 31 days, in the worst case), but the data's been prepared for me within a few minutes when I've requested it.

Garmin's bundles raw data in a difficult-to-parse format called `.fit`, but that's a trade-off I'm willing to make in exchange for Garmin curating, hosting, and making what comes off the device directly available to me (albeit, as a compliance measure, but still).

The `.fit` situation is not as bad as it could be.
The file format specifications and some developer tools, including a tool to convert `.fit` to `.csv`, are [available freely](https://www.thisisant.com/resources/fit/).

That said, the `.fit` files are full of fun [undocumented ](https://www.thisisant.com/forum/viewthread/6374), [cryptic](https://forums.garmin.com/forum/on-the-trail/wrist-worn/fenix-5-5s/1375156-hrv-data-replaced-by-unknown-data-in-fit-files), and [nonstandard](https://forums.garmin.com/forum/into-sports/cycling/1245820-how-to-convert-timestamp) easter eggs.
Although the `.fit` data file standard's specifications are nominally made available, how exactly the engineering team behind the Vivosmart 3 *uses* that standard *definitely* is not.

On a cursory inspection, though, it looks like I should be able to wring enough data out of these `.fit` files to tell an interesting story.
Here's an excerpt of one of the raw log files from the device, which I converted to a CSV using the `FitCSVTool.jar` Java JAR file from the SDK.

<script src="https://gist.github.com/mmore500/c9e4f1147f12bc745a3ecdf4f761646e.js"></script>

Also in the GDPR dump, a nice JSON file that seems to summarize sleep information.

<script src="https://gist.github.com/mmore500/4ce2d45bba21bb0eeb46eeb7af02c81c.js"></script>

So, my post-hoc rationalization for using a Garmin device is that the company is reasonably [likely to exist in a few years years](https://finance.yahoo.com/quote/FIT/chart?p=FIT#eyJpbnRlcnZhbCI6IndlZWsiLCJwZXJpb2RpY2l0eSI6MSwiY2FuZGxlV2lkdGgiOjYuNDg1NzE0Mjg1NzE0Mjg2LCJ2b2x1bWVVbmRlcmxheSI6dHJ1ZSwiYWRqIjp0cnVlLCJjcm9zc2hhaXIiOnRydWUsImNoYXJ0VHlwZSI6ImxpbmUiLCJleHRlbmRlZCI6ZmFsc2UsIm1hcmtldFNlc3Npb25zIjp7fSwiYWdncmVnYXRpb25UeXBlIjoib2hsYyIsImNoYXJ0U2NhbGUiOiJsaW5lYXIiLCJwYW5lbHMiOnsiY2hhcnQiOnsicGVyY2VudCI6MSwiZGlzcGxheSI6IkZJVCIsImNoYXJ0TmFtZSI6ImNoYXJ0IiwidG9wIjowfX0sInNldFNwYW4iOnsiYmFzZSI6ImFsbCIsIm11bHRpcGxpZXIiOjF9LCJsaW5lV2lkdGgiOjIsInN0cmlwZWRCYWNrZ3JvdWQiOnRydWUsImV2ZW50cyI6dHJ1ZSwiY29sb3IiOiIjMDA4MWYyIiwiZXZlbnRNYXAiOnsiY29ycG9yYXRlIjp7ImRpdnMiOnRydWUsInNwbGl0cyI6dHJ1ZX0sInNpZ0RldiI6e319LCJjdXN0b21SYW5nZSI6bnVsbCwic3ltYm9scyI6W3sic3ltYm9sIjoiRklUIiwic3ltYm9sT2JqZWN0Ijp7InN5bWJvbCI6IkZJVCJ9LCJwZXJpb2RpY2l0eSI6MSwiaW50ZXJ2YWwiOiJ3ZWVrIiwidGltZVVuaXQiOm51bGwsInNldFNwYW4iOnsiYmFzZSI6ImFsbCIsIm11bHRpcGxpZXIiOjF9fV0sInRpbWVVbml0IjpudWxsLCJzdHVkaWVzIjp7InZvbCB1bmRyIjp7InR5cGUiOiJ2b2wgdW5kciIsImlucHV0cyI6eyJpZCI6InZvbCB1bmRyIiwiZGlzcGxheSI6InZvbCB1bmRyIn0sIm91dHB1dHMiOnsiVXAgVm9sdW1lIjoiIzAwYjA2MSIsIkRvd24gVm9sdW1lIjoiI0ZGMzMzQSJ9LCJwYW5lbCI6ImNoYXJ0IiwicGFyYW1ldGVycyI6eyJ3aWR0aEZhY3RvciI6MC40NSwiY2hhcnROYW1lIjoiY2hhcnQifX19fQ%3D%3D) and, unexpectedly provides access to raw `.fit` files, which are decently well-documented due to GDPR, which probably isn't going away soon.
That said, I went ahead and cached a copy of the [FIT SDK 20.76.00](https://osf.io/my2sk/), you know, just in case.

## Manual Biometrics Logging

I track my weight using an [If This Then That (IFTTT)](https://ifttt.com/) SMS to Google Sheets recipe.
I just text the IFTTT messages like `#w XXX.X` to add an entry
I like being able to add entries from anywhere and having 100% control over how this data is stored.

You can see the recipe I use [here](https://ifttt.com/applets/ukbVqRhA-log-weight-via-sms).

If you have other biometrics you want to track (like your PR's, brodawg), it's easy to set up similar recipes that just use other hashtag codes.

## Journal

I've already rambled about my journaling tool elsewhere [on my blog](https://mmore500.github.io/2018/01/21/my-record-keeping-setup.html).

I'm pleasantly surprised with how well my system seems to be working out for me.
A bit more than a year after I started, I still do things the same way.

I've returned to my journal to dig up details I had otherwise forgotten for [anecdotes I wanted to re-tell](http://devosoft.org/reflections-on-my-first-semester-at-macdonald-middle-school/).

## Social Media

At the moment, I don't anticipate data on my social media activity would be particularly interesting to analyze, but who knows.
It's *definitely* being collected and stored!
If I ever really wanted it, I might be able to GDPR the data.

Email would probably be the most likely candidate for interesting personal analytics.
If you use google mail, you're [probably covered with respect to data portability](https://support.google.com/accounts/answer/3024190?hl=en).

## Manual Data Management

Now that I have all these great log files plugging away on my laptop, where should I shunt the data off to as it accumulates?
Right now, I think I'll just throw it onto the two external hard drives I keep for my photos (one at work and the other at home).
I wouldn't be devastated if I were to lose my laptop logs, so I don't think I'll bother keeping a third off-site copy.

Right now, I think I can handle moving three logfiles to my external hard drives once a month, especially as I make archives there on a monthly basis anyways as part of [my photography workflow](https://mmore500.github.io/2018/01/22/my-photography-workflow.html).
I set myself a recurring reminder, so at least I'll know I'm dropping the ball if I don't keep up with it.

## Let's Chat

I would love to hear your own thoughts about and experiences with personal analytics!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">✨new✨ blog post about setting up self-loggers for personal analytics fun!<a href="https://t.co/tPbiYViOZY">https://t.co/tPbiYViOZY</a><br><br>enjoy 😺</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1067589873429897217?ref_src=twsrc%5Etfw">November 28, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish:, make a comment :raising_hand_woman:, or leave your own tips & tricks :heart:
