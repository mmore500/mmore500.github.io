---
layout: post
title:  "Setting Up Self-Loggers"
date:   2018-10-12
---

<!-- make sure that Gist snippets don't display too tall -->
<style type="text/css">
  .gist {!important;}
  .gist-data{
      max-height:250px;
      overflow-y: visible;
  }
</style>

A few weeks ago, I passed my comprehensive exam.
I finish up my coursework this spring.
So, I've been in the mood to look forward.
Looking forward, of course, means looking towards the dissertation.

I tend to see purpose as an echo of function.
On average, [1.6 people read a PhD thesis all the way through --- including the author](https://www.nature.com/news/the-past-present-and-future-of-the-phd-thesis-1.20207).
In most cases, the function of the thesis itself isn't as a vessel for scientific knowledge.
[The function of the thesis --- its existential purpose --- is self-growth.](
https://www.nature.com/news/back-to-the-thesis-1.20202)
At risk of stating the obvious, the thesis is an artifact of graduate education.

When I finish up my dissertation, I'd like to be able to tell a neat story about putting it together.
For my own benefit, I hope that experiencing the process as much as possible as an opportunity for personal growth through a challenge instead of as a harrowing, arbitrary hoop to jump through.
I also hope that documenting and sharing my own process might lift the shroud around graduate education and make it seem approachable for students who are unfamiliar with the annals of academia.

I'm a big believer in the [utility of narrative reflection](http://devosoft.org/reflections-on-my-first-semester-at-macdonald-middle-school/).
However, I anticipate that baking in data will yield an even more compelling story.
I'm inspired by the stories [Kazuo Yano](http://gecco-2018.sigevo.org/index.html/tiki-index.php?page=Keynotes) and [Steven Wolfram](https://www.glassdoor.com/Reviews/Wolfram-Research-Reviews-E14501.htm) have told, respectively, via nifty [wrist-accelerometer data](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.497.4009) and  [phone/email/keylogger/more data](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/).
I hope data describing my process will lend invigorating detail to the narrative and perhaps even point my thinking in directions I wouldn't have considered otherwise.
Cute statistics and nifty visualizations make good buzz marketing fodder on academic twitter, too. :wink:


Of course, in order to live out that dream, I need to set myself up with data to play with when the time arrives.

## Key Logger

I chose to use [logkeys](https://github.com/kernc/logkeys).
Although, in [their README](https://github.com/kernc/logkeys/blob/master/README.md), the package very modestly plugs other Linux key logging software, after a few minutes' worth of poking around on Google it seems to be the only reasonably maintained option.

I also considered [SelfSpy](https://github.com/selfspy/selfspy), which is a bit more than just a keylogger.
SelfSpy also tracks mouse movement and which window you have in focus.
Its killer feature is the well-developed suite of analysis tools packaged with it that work seamlessly.
In my very cursory judgment, the amount recent development activity underwhelms its heavy footprint.
I figured I'd have a better chance of collecting a continuous stream of data (or, realistically, more useful patchy data) over the time-frame of years with logkeys.
Plus, I had a bad time trying to get SelfSpy going as a background process and gave up.

### Logkeys with Multiple Keyboards

Now, that's not to say that setting up logkeys didn't involve its own set of fire-y hoops to jump through.

I use an [external keyboard](https://ergodox-ez.com/) when I work on my work laptop at my desk.
If your machine is a desktop computer with just one keyboard, you can install logkeys as usual (e.g., perhaps `sudo apt-get install logkeys`) and skip this subsection.
Otherwise, getting logkeys going takes a little more work.

Luckily for us, [bryan-hoyle](https://github.com/bryan-hoyle) already did the heavy lifting.
He wrote [a patch for logkeys](https://github.com/kernc/logkeys/tree/bace087155e7c54293d44341fa552fb229d588ac) that allows logkeys to multiplex input from several keyboards.
Unfortunately, as of October 2018, [his pull request](https://github.com/kernc/logkeys/pull/171) to bring the fixes into `master` has been gathering dust for a full year.
So, you'll need to install logkeys from the tip of his development branch instead of from `master`.

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

As inevitable in software install sagas, another misfortune befalls us: logkeys keyboard multiplexing seems to require on keyboards availability at startup.
That means, when we plug in or unplug an external keyboard, we need to re-launch `logkeys` in order to ensure correct logging (e.g., not completely ignoring input from an external keyboard or incorrectly double-entering input from the laptop board after the external keyboard is unplugged).

Ideally, we'd just hook logkeys restarts into keyboard plug-in/unplug events via `/etc/udev/rules.d/`.
Unfortunately, I found that hooking logkeys launch into keyboard plug-in events interfered with keyboard set-up, causing dead external keyboard input.
I have no idea why.

After an hour or two of whack-a-mole trial and error, I settled on a workable (although not totally idea) solution:
1. having a keyboard connect/disconnect event kill the currently running logkeys process
2. using crontab to *attempt* logkeys launch every few seconds (if logkeys is currently running, no action is taken)

To accomplish part 1 of the solution, I created a new entry `/etc/udev/rules.d/100-mount-ergodox.rules` (you can replace `ergodox` with whatever you prefer to refer to your own keyboard as) containing the following rules

~~~
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="feed", ATTRS{idProduct}=="1307", RUN+="/usr/local/bin/logkeys -k"
ACTION=="remove", SUBSYSTEM=="usb",  RUN+="/usr/local/bin/logkeys -k"
~~~

In this snippet, `feed` and `1307` are the hex codes specifying my external keyboard's vendor and model.
To get your keyboard's vendor and model, run `lsusb` with your external keyboard unplugged,

~~~
lsusb
~~~

then plug in your external keyboard and run `lsusb` again.
The entry that appeared contains the hex codes specifying your keyboard's vendor and model.

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
You'll need to switch out `/home/mmore500/.config/logkeys/mylang.map` with whatever path you put your custom keymap on.
If you didn't need to make a custom keymap, you can omit `-m /home/mmore500/.config/logkeys/mylang.map`.
([See below](#SmartHome) for details on testing whether you need a custom keymap and setting one up.)

I call the `logkeys-start.sh` script via crontab every five seconds.
This way, logkeys will promptly restart after keyboard plug-in/unplug events kill it.
When logkeys, is running, calling `logkeys -s` has no effect.
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

### Logkeys Keymap <a name="LogkeysKeymap"></a>

I run [elemenary OS](https://elementary.io/) on a [Lenovo Thinkpad Carbon](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/ThinkPad-X1-Carbon-5th-Gen/p/22TP2TXX15G).
In order to get correct key log output, I had to define a custom keymap.

If you're lucky, you might not have to worry about this detail, either!
Try this to check if you might need a custom keymap.
Start logkeys up with the default keymap.
~~~
logkeys -s
~~~

Now, open a peek into the key log.
~~~
sudo tail /var/log/logkeys.log --follow
~~~

Then, go somewhere else to push every single button on your keyboard keep an eye on the key log.
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

As before, check if, under the custom keymap, what shows up in the log matches what you're pressing.
Continue to make changes as needed, restarting logkeys each time, and trial-and-error your way to glory.
Here's what my keymap ended up looking like.

<script src="https://gist.github.com/mmore500/1dcfc0813c88b5e383f9bbb72914e918.js"></script>

I arbitrarily keep it at `~/.config/logkeys/mylang.map`.

For more details on the logkeys keymap, [see here](https://github.com/kernc/logkeys/blob/master/docs/Keymaps.md).

### Security

If you set up a keylogger on your computer, that means... you're running a keylogger on your computer, yo.
All of your passwords and [your dirty, dirty secrets](https://andburch.github.io/selfspy/) are recorded in a file someone else might be able to get their hands on.
If you work with sensitive information, there are probably rules you might want to make sure you're not breaking.

On the flip side of the coin, recording everything might be useful for, probably with some elbow grease, recovering lost work in the event of a deletion disaster.

## Keyboard Connect/Disconnect Logger

Hooking into keyboard connect/disconnect events to make `logkeys` work, I realized that they keyboard connect/disconnect events might tell an interesting story in and of themselves.
If my keyboard is plugged in, that's a pretty good sign I'm working at my desk.
Otherwise, I'm probably enjoying a bespoke espresso at my favorite upscale coffee shop.
(Hahahahaha, no, I'm working in bed).

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
They'll run every time I unplug a usb device.
That's why I threw the output of `lsusb` into `log-plugout.sh`.

Again, you'll need to reboot or reload the `udev` rules to get these hooks running.
~~~
udevadm control --reload-rules && udevadm trigger
~~~

## Wi-Fi Logger

I have two desks --- one at work and one at home.
I realized I might want to be able to tell which desk I'm working at.
The answer to recognizing which desk I'm at: which Wi-Fi signal I'm on.
Which Wi-Fi I'm on should tell other interesting stories, too, like how much work I do on versus off campus.

Here's the script.

<script src="https://gist.github.com/mmore500/a4c4d0dae5cae303d9006bbf2fab538d.js"></script>

Apparently, it's important for this one to not end in `.sh`.

## Document Logger

In what order over time did a document/codebase come together?

![](http://blog.stephenwolfram.com/data/uploads/2012/03/NKSBookMods-1991r.png)

If you use a version control system like `git`, you should already be collecting the information you need to answer a question like this!

Your commit history can tell a story about yourself, too, not just a document.
GitHub already stitches together your commit pattern across projects to make neat annual visualizations.

![](https://osf.io/4dn2q/download)

I can see time off for winter break and a few deadlines on this one from 2018.
In contrast, my advisor maintains a [very impressive 365/365 record](https://github.com/mercere99)
You can find yours on your Github profile.

## Calendar

If you use a calendar,

## Photos


At least to The archive view
archive view http://mmore500.tumblr.com/archive

The content of the photos themselves probably tell the richest story, but I'm sure there are other .

glorious, glorious metadata
+ aperture
+ time of day
+ shutter count

[my photography workflow](https://mmore500.github.io/2018/01/22/my-photography-workflow.html)

## Fitness Trackers

Garmin devices because they're cheap and I liked the sensor suite.
The [device I use](https://www.amazon.com/gp/product/B07BH3XN3T/ref=oh_aui_detailpage_o03_s00?ie=UTF8&psc=1) has:
* heart rate sensor
* accelerometer
* altimeter

No GPS, which is fine by me.

My post-hoc rationalization is that Garmin is reasonably [likely to exist in four years years](https://finance.yahoo.com/quote/FIT/chart?p=FIT#eyJpbnRlcnZhbCI6IndlZWsiLCJwZXJpb2RpY2l0eSI6MSwiY2FuZGxlV2lkdGgiOjYuNDg1NzE0Mjg1NzE0Mjg2LCJ2b2x1bWVVbmRlcmxheSI6dHJ1ZSwiYWRqIjp0cnVlLCJjcm9zc2hhaXIiOnRydWUsImNoYXJ0VHlwZSI6ImxpbmUiLCJleHRlbmRlZCI6ZmFsc2UsIm1hcmtldFNlc3Npb25zIjp7fSwiYWdncmVnYXRpb25UeXBlIjoib2hsYyIsImNoYXJ0U2NhbGUiOiJsaW5lYXIiLCJwYW5lbHMiOnsiY2hhcnQiOnsicGVyY2VudCI6MSwiZGlzcGxheSI6IkZJVCIsImNoYXJ0TmFtZSI6ImNoYXJ0IiwidG9wIjowfX0sInNldFNwYW4iOnsiYmFzZSI6ImFsbCIsIm11bHRpcGxpZXIiOjF9LCJsaW5lV2lkdGgiOjIsInN0cmlwZWRCYWNrZ3JvdWQiOnRydWUsImV2ZW50cyI6dHJ1ZSwiY29sb3IiOiIjMDA4MWYyIiwiZXZlbnRNYXAiOnsiY29ycG9yYXRlIjp7ImRpdnMiOnRydWUsInNwbGl0cyI6dHJ1ZX0sInNpZ0RldiI6e319LCJjdXN0b21SYW5nZSI6bnVsbCwic3ltYm9scyI6W3sic3ltYm9sIjoiRklUIiwic3ltYm9sT2JqZWN0Ijp7InN5bWJvbCI6IkZJVCJ9LCJwZXJpb2RpY2l0eSI6MSwiaW50ZXJ2YWwiOiJ3ZWVrIiwidGltZVVuaXQiOm51bGwsInNldFNwYW4iOnsiYmFzZSI6ImFsbCIsIm11bHRpcGxpZXIiOjF9fV0sInRpbWVVbml0IjpudWxsLCJzdHVkaWVzIjp7InZvbCB1bmRyIjp7InR5cGUiOiJ2b2wgdW5kciIsImlucHV0cyI6eyJpZCI6InZvbCB1bmRyIiwiZGlzcGxheSI6InZvbCB1bmRyIn0sIm91dHB1dHMiOnsiVXAgVm9sdW1lIjoiIzAwYjA2MSIsIkRvd24gVm9sdW1lIjoiI0ZGMzMzQSJ9LCJwYW5lbCI6ImNoYXJ0IiwicGFyYW1ldGVycyI6eyJ3aWR0aEZhY3RvciI6MC40NSwiY2hhcnROYW1lIjoiY2hhcnQifX19fQ%3D%3D) and I bet I'll still be able to access the RAW `.fit` files throughout.

Thanks to [GDPR](https://forums.garmin.com/forum/into-sports/garmin-connect/feature-requests/1343456-download-of-all-health-data-as-required-under-gdpr).
Maybe being [spammed for months on end](https://xkcd.com/1998/) earlier this year was worth something.

It's not actually baked into their [main interface](https://connect.garmin.com/modern/) but is available through their ["account manager"](https://www.garmin.com/en-US/account/profile/).
You have to request a data export and then wait while they prepare it.
They claim you should expect to wait two days (and up to 31 days, in the worst case), but it's been prepared for me within a few minutes when I've requested it.

The data is in a difficult-to-parse format, but that's a trade-off I'm willing to make for Garmin making what comes off the device directly available to me, curating it, and hosting it.
Also, having the raw

share data (fitness tracker)
FIT files nightmare

A protocol called [ANT](https://www.thisisant.com/), which was created by a Canadian company called Dynastream that Garmin bought out in 2006.

You can find the SDK for FIT, which includes some documentation for the standard, [here](https://www.thisisant.com/resources/fit/).

The `.fit` files are full of fun [undocumented ](https://www.thisisant.com/forum/viewthread/6374), [cryptic](https://forums.garmin.com/forum/on-the-trail/wrist-worn/fenix-5-5s/1375156-hrv-data-replaced-by-unknown-data-in-fit-files), and [nonstandard](https://forums.garmin.com/forum/into-sports/cycling/1245820-how-to-convert-timestamp) bits, but on a cursory inspection it looks like I should be able to get what I want out of it.

I posted an excerpt of what seems to be one of the [raw log files from the device](https://gist.github.com/mmore500/c9e4f1147f12bc745a3ecdf4f761646e), which I converted to a CSV using the `FitCSVTool.jar` Java JAR file from the SDK.

<script src="https://gist.github.com/mmore500/c9e4f1147f12bc745a3ecdf4f761646e.js"></script>

Also in the GDPR dump, [a nice JSON file](https://gist.github.com/mmore500/4ce2d45bba21bb0eeb46eeb7af02c81c) that seems to summarize sleep information.

<script src="https://gist.github.com/mmore500/4ce2d45bba21bb0eeb46eeb7af02c81c.js"></script>

I went ahead and cached a copy of the [FIT SDK 20.76.00](https://osf.io/my2sk/), you know, just in case.

## Manual Biometrics

I track my weight using an If This Then That (IFTTT) SMS to Google Sheets recipe.
I like having 100% control over this data and being able to add data from anywhere.
You can see the recipe I use [here](https://ifttt.com/applets/ukbVqRhA-log-weight-via-sms).

## Journal

I've already talked about how I like to do this [on the blog](https://mmore500.github.io/2018/01/21/my-record-keeping-setup.html).
The system seems to be working out pretty well for my personal taste.
A bit more than a year after I started, I still do things the same way.

I don't think that there's particular

I've already [found it useful](http://devosoft.org/reflections-on-my-first-semester-at-macdonald-middle-school/).

I've toyed around with the idea of publishing these after the fact.

## Social Media

I'm not particularly interested, at the moment, but it's out there.

Probably gdpr it.

If you use google products, you're [probably covered](https://support.google.com/accounts/answer/3024190?hl=en).

## Manual Data Management

Where to store the data?
Right now, I think I'll just plop it onto the two external hard drives I keep for my photographs (one at work and the other at home).
link
I wouldn't be devastated if I were to lose it, so I don't think I'll bother keeping a third off-site copy.

I set myself a reminder.
Right now, I think I can handle moving three logfiles to my external hard drives once a month, especially as I make archives there on a monthly basis anyways as part of [my photography workflow](https://mmore500.github.io/2018/01/22/my-photography-workflow.html).

## Let's Chat

I would love to hear your own thoughts about and experiences with personal analytics!!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">nothing to see here, just a placeholder tweet 🐦</p>&mdash; Matthew A Moreno (@MorenoMatthewA) <a href="https://twitter.com/MorenoMatthewA/status/1054071480512843776?ref_src=twsrc%5Etfw">October 21, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish:, make a comment :raising_hand_woman:, or leave your own tips & tricks :heart:
