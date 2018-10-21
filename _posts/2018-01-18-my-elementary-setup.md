---
layout: post
title:  "My Elementary Setup"
date:   2018-01-18
---

I use [elementary OS](https://elementary.io).

I *really* like using elementary OS.
The interface has come to feel like a good pair of boots, broken in to fit just right.

How many hours have I spent aimlessly stomping around to break in these boots?
You probably don't want to know.
I certainly don't want to --- I'm not really in the mood for an existential crisis right now.

What I do hope you want to know about are some of the tweaks and enhancements I made to make elementary look and work just how I like.
If not, go read something else.

Everything below assumes Version 0.4.1 Loki.

## Remove Guest Account from Login Screen

I got tired of looking at the guest account option on the beautiful elementary login screen.
Even though I had disabled the guest account itself, the icon remained.
I decided to get rid of it.

Totally pointless?
Certainly.
Extremely satisfying?
Definitely.

To fix this issue, I opened up the configuration file `/etc/lightdm/lightdm.conf` and modified the line `allow-guest=false` to instead read `allow-guest=true`.

Note that you might need superuser permissions to modify this file (i.e. `sudo`).

## Redshift

Until elective surgery for HDMI input implants gains widespread availability, I'll continue to need my eyeballs to look at my computer screen.
Plus, they're useful for [other things](http://mmore500.tumblr.com/), too.

Blue light hurts my eyes, especially at night when I'm at home sleeping at night and definitely not still at the office my computer.
I try to give my retinas a break by cutting back on the amount of blue light I'm shining in my face at all hours.
[f.lux]([https://justgetflux.com/) does a great job of warming the screen color on the mac, but its Linux port doesn't cut it.
Use [Redshift](https://github.com/jonls/redshift) instead.

## Guake

At some point, I got tired of having 50 random terminals open all the time.
So, I installed [Guake](https://github.com/Guake/guake), which lets you use a hotkey shortcut to drop down a floating terminal from the menu bar.


I use the "Space Gray" color scheme.
It's pretty rad.

## Remap Modifier Keys

I migrated to Elementary OS from Mac OS.
Given my long history with apple, I was strongly conditioned to use the <kbd>&#8984;</kbd> key to do things that the <kbd>ctrl</kbd> does for me now (e.g. <kbd>&#8984;</kbd> + <kbd>C</kbd> to copy text on mac vs. <kbd>ctrl</kbd> + <kbd>C</kbd> to copy text in elementary).
For a while, I didn't want to recondition myself because I used both systems regularly.
Now, even though I use elementary exclusively, reconditioning myself would just be too traumatic.

The solution here is to remap input from your keyboard.
That way, you can hit the physical <kbd>cmd</kbd> or <kbd>&#8984;</kbd> key on your keyboard but have the operating system perceive it as a <kbd>ctrl</kbd> press.


What I learned in boating school is there are a lot of ways to try to achieve this that don't work.
Forget `.Xmodmap`.
You'll need to work with X KeyBoard extension files.
To change your modifier key (i.e. <kbd>ctrl</kbd>, <kbd>alt</kbd>, <kbd>cmd</kbd>) mappings you'll want to poke around in `/usr/share/X11/xkb/symbols/pc`.
Note that you might need superuser permissions to modify your `pc` file (i.e. `sudo`).

For example, to map your physical right-<kbd>alt</kbd> key to mean right-<kbd>ctrl</kbd> to your operating system, change the line
```
key <RALT> {  [ Alt_R ] };
```
to read
```
key <RALT> {  [ Control_R ] };
```

To remap your physical right-<kbd>ctrl</kbd> key to mean right-<kbd>cmd</kbd> (a.k.a. <kbd>super</kbd>), change the line
```
key <RCTL> {  [ Control_R ]  };
```
to read
```
key <RCTL> {  [ Super_R ]  };
```

My personal keymapping probably isn't too useful to you because my physical keyboard is laid out kinda funky.
(Among other tweaks, I had to remap <kbd>PrtSc</kbd> to <kbd>alt</kbd>).
For whatever you can make out of it, though, it's [here](https://gist.github.com/mmore500/12c5eee702815bc0167b808c584c6639#file-pc-L62).

You'll need to log out and log back in to see your changes take effect.
You might have to reboot or do some cache clearing as described [here](http://www.fascinatingcaptain.com/blog/remap-keyboard-keys-for-ubuntu/) if your changes aren't taking effect as they should.

## Hide Mouse Cursor

Give yourself a fighting chance in your own valiant struggle to ditch the mouse by hiding the cursor when it's not being used.

You'll need to install the [unclutter](https://wiki.archlinux.org/index.php/unclutter) package.
```
sudo apt-get install unclutter
```

You can then test unclutter out at the command line.
```
unclutter -idle 0.1 -root
```

To get unclutter to run in the background at startup, paste this into your `~/.xintrc`.
(If you don't have an `~/.xintrc` file, make one.)
```
unclutter -idle 0.1 -root &
```

## Uninstall Unused Elementary Built-Ins

Elementary's built-in mail, calendar, photos, music, etc. software is a nice gesture.
I don't use them, though, and I doubt many others do either.

To remove unused built-in software, open AppCenter and locate an application you don't use via the search bar.
Click to open that application's product description page.
You should see an option to uninstall.
Click it then rinse and repeat for everything else you want gone.

## Remove Unused Shortcuts from Slingshot Launcher Menu

If you're bothered by clutter in your application launcher menu, then at least I'm not the only one.
Command-line software that comes packaged with a desktop application interface especially bothers me.
The culprit are `*.desktop` files in any of these three locations:

* `/usr/share/applications`,
* `/usr/local/share/applications`, and
* `~/.local/share/applications`.

You'll need to poke through these directories until you find the offender.
Then, remove it.
You won't be able to open the application from the GUI launcher anymore, but command line components (and windowed components launched from the command line) should continue to work just fine.

For example,
```
cd /usr/share/applications
sudo rm ufraw.desktop
```
If no `*.desktop` files jumps out as the culprit, you might need to start peeking in suspect `*.desktop` files to check for the name and description of the application.
Note that you might need superuser permissions to remove files under the `/usr` directory (i.e. `sudo`).

(Original source [here](https://askubuntu.com/questions/71240/how-to-remove-icons-shortcuts-from-unity-menu).)

## Block Distracting Websites <a name="BlockDistractingWebsites"></a>

One of my friends works at a municipal library in small-town middle America.
On her performance review, anonymous coworker told her that she needed to cool her jets because she was making everyone else look bad.
According to this coworker, "Just because we have Facebook open our computers most of the time doesn't mean we're not as good as you.
We just work differently."

Don't be my friend's anonymous passive-aggressive colleague.
Redirect your outgoing traffic to distracting/dumb websites to a dead end instead.

To do this you'll need to modify `/etc/hosts`, which your computer uses to decide where to look for certain web addresses.

I've compiled a pretty comprehensive listing of distracting sites in [my own `/etc/hosts` file](https://gist.github.com/mmore500/0246a16142532e72d56167e905733d69).
If you like, you can just paste this over your own `/etc/hosts`.
Or, just add entries of the following format to the end of your `/etc/hosts` that block your own [clickholes](http://www.clickhole.com/).

```
127.0.0.1 clickhole.com
```

Note that you might need superuser permissions to modify this file (i.e. `sudo`) and you might need to reboot to see changes take place.

## Dark Theme for Elementary

Go check out [elementary tweaks](https://github.com/elementary-tweaks/elementary-tweaks).

## Replace Applications with Elementary Logo

Want to replace the "Applications" text on the wingpanel bar with the elementary OS logo?

Totally pointless?
Certainly.
Extremely satisfying?
Definitely.

Check out `nightsense`'s [elementary-panel-logomark project](https://github.com/nightsense/elementary-panel-logomark).
Also, consider using the inverse logo I contributed.
It has less negative space than the original so it displays better.

Good usage instructions are provided on the project's `README.md`.

## Weather Widget

[Conky](https://github.com/brndnmtthws/conky) is a widget that lets users display system information on their desktop.
Conky-vision is a stylish theme that puts the current time, date, and five-day forecast on the desktop..
The code for Conky-vision, due to `zagortenay333`, is found [here](https://github.com/zagortenay333/conky-Vision).
Good installation and configuration instructions are on the project's README.md.

You might want to check out [my branch](https://github.com/mmore500/conky-Vision/tree/elementary).
I added elementary-specific font that matches the login greeter.

## Use 24-Hour Clock on the Login Screen

Want the elementary greeter to respect your system preferences and display a 24-hour clock if that's your preferred time format?

Totally pointless?
Certainly.
Extremely satisfying?
Definitely.

At least this time I know I'm not the only one bothered by this.
You can see the issue on github [here](https://github.com/elementary/greeter/issues/52).
There's even a [pull request](https://github.com/elementary/greeter/pull/53) up with a fix.
As of January 2018, though, the pull request remains unmerged.

I'm impatient, so I grabbed the unmerged code from [here](https://github.com/vjr/greeter/tree/fix-time-format) and compiled/installed greeter from source according to the instructions on the project's `README.md`.

## Transparent Wingpanel Bar

A totally transparent (not partially translucent) wingpanel bar can be achieved by hacking on the CSS that's used to style elementary.
(Wingpanel is the menu bar at the top of your screen that displays the time, holds indicators for some apps, opens the slingshot application launcher, and lets you monitor the volume, wi-fi connectivity, bluetooth connectivity, battery status, etc. of your machine).
The relevant CSS code is found at `/usr/share/themes/elementary/gtk-3.0/apps.css`.

Find a copy of my modified `apps.css` file  [here](https://gist.github.com/mmore500/76f68ed98b3d69bae2dc61f02f35df56).
Note that you might need superuser permissions to save modifications to your `apps.css` file (i.e. `sudo`).

## Translucent Slingshot Launcher Menu

At some point, I decided that I wanted (needed?) the slingshot launcher menu to be slightly translucent.
This also required hacking on the CSS that's used to style elementary.
For this, the CSS I manipulated was actually in a supplementary file associated with elementary tweaks' dark theme (mentioned above).
The CSS is located at `/usr/share/themes/elementary/gtk-3.0/gtk-dark.css`.

Find a copy of my modified `gtk-dark.css` file [here](https://gist.github.com/mmore500/2e25e9f14ee12b266d2cc968f68ba7ab).
Note that you might need superuser permissions to save modifications to your `gtk-dark.css` file (i.e. `sudo`).

As a side effect, the change I made to give the launcher menu some translucency also makes some of the elementary's system window backings slightly translucent.
I like this effect, but if it's not for you skip this one.

## Unfulfilled Dream: Lenovo Fingerprint Sensor Support

This really is a hardware issue that has nothing to do with elementary, but Lenovo provides no linux driver support for the fingerprint reader on my X1 Carbon Thinkpad.
If you're in the same boat, our last best chance is an [unofficial effort to reverse engineer the necessary drivers](https://github.com/nmikhailov/Validity90).
Despite plenty of cheerleaders on the sidelines, it doesn't look like the project's going anywhere fast.
Nevertheless, hope springs eternal...

## Bonus: `.bash_profile`

Nate Landau's `.bash_profile`: kick-ass.
There are all kinds of little gems in there that will make you such happy and much productive at the terminal.
Read his [blog post](https://natelandau.com/my-mac-osx-bash_profile/) about it or just skip over to [the main attraction](https://gist.github.com/natelandau/10654137).
Highly recommended.
To use Nate's `.bash_profile` magic, paste the content into your `~/.bash_profile`.

Playing with my bash prompt was my first foray into excessive personalization of my computing environment.
Really, though, who cares if you spend an hour or two tinkering with your bash prompt?
Chances are, if you're still reading this you'll be tooling around in bash everyday for the next decade or more.
I'll certainly be.
You deserve a rad-tastic bash prompt.
So go ahead and Treat. Yo. Self.

For kicks, here's the code I use to define my own bash prompt.

```
export PS1="\[\e[32m\]\e[1m\#\[\e[0m\]//\[\e[32m\]\e[1m\A\[\e[0m\]//\[\e[32m\]\e[1m\u\[\e[0m\]:\[\033[01;34m\]\e[1m\W\[\e[0m\]\$ "
```

It renders as
```
10//21:02//username:Directory$
```
where `10` is the count of commands executed so far in this terminal session, `21:02` is the time the prompt was created, `username` is your username, and `Directory` is the name of the directory you're currently sitting in.
To boot, the prompt is styled with nice colors and nice bold weight that you can't see here.
Feel free to take and [modify as you see fit](https://ss64.com/bash/syntax-prompt.html).
To use it, paste the line `export PS1=...` into your `~/.bash_profile`.

## Bonus Bonus: Vimium and Momentum for Chrome

How did I live before I could navigate the web without my mouse?
I certainly couldn't now.
Vimium is a nifty extension for Chrome that, at your request, will render dynamic hotkeys on top of all of the clickable elements of whatever webpage you're browsing.
It's basically magic.
Find it [here](https://github.com/philc/vimium).

The Momentum Chrome extension will also help make your desk-jockey existence more tolerable.
It says something nice to you, shows you a pretty picture, and reminds you what time it is when you open a new tab.
Really, what more can you ask for?
Get it [here](https://momentumdash.com/).
