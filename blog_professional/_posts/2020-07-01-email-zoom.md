---
layout: post
title:  "Life Hacks RE: Too Much Zoom & Too Much Email"
date:   2020-07-01
---

## You've Got Mail!

Ah, email.
How do I love thee?
Let me count the ways.

None.
Zero ways.

Pick an academic of your choice with a twitter.
Search their username and the word "email."
Enjoy the snarky 2 to 7+ tweets that appear.

I've curated a few of my favorites here.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I wonder how many emails I’ve received in my life probably at least four maybe five</p>&mdash; darren i (@MegaDarren) <a href="https://twitter.com/MegaDarren/status/1190404689071878144?ref_src=twsrc%5Etfw">November 1, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I am honestly shocked at this dominance by “Best.” It has always felt a bit pretentious to me. But, then again, who am I to judge. I used to sign all my emails with “Enjoy” until my grad school advisor staged an intervention in my fourth year. <a href="https://t.co/X1pDZYyWdq">https://t.co/X1pDZYyWdq</a></p>&mdash; David B. Lowry (@DavidBLowry) <a href="https://twitter.com/DavidBLowry/status/1127999495101407233?ref_src=twsrc%5Etfw">May 13, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">My email filters are pretty good does that count? <a href="https://t.co/7R77Zx0b6D">https://t.co/7R77Zx0b6D</a></p>&mdash; Tess Huelskamp (@TessHuelskamp) <a href="https://twitter.com/TessHuelskamp/status/1202617466683154433?ref_src=twsrc%5Etfw">December 5, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I went out on my lunch break for &lt; 30 mins and I come back to TEN. NEW. EMAILS. How are any adults productive ever?? Good lord!!</p>&mdash; Lauren Gilles (@leg2015) <a href="https://twitter.com/leg2015/status/1181297916192755712?ref_src=twsrc%5Etfw">October 7, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">used my extensive &amp; rigorous training in quantitative methods to run some quick back-of-the-napkin math 🤓📊🤷‍♂️<br><br>&amp; 100,000 is at least half an order of magnitude more than the number of listserv and grad chair fwd fwd fwd FYI emails I will delete over 5 years at msu <a href="https://twitter.com/hashtag/stayhome?src=hash&amp;ref_src=twsrc%5Etfw">#stayhome</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1244648799240257536?ref_src=twsrc%5Etfw">March 30, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Thank you for emailing Hiroki Sayama. All the Hirokis are currently assisting other customers. Your inquiry is very important to me; please stay online and I will reply to your emails in the order they were received.</p>&mdash; Hiroki Sayama (@HirokiSayama) <a href="https://twitter.com/HirokiSayama/status/1220113409703702534?ref_src=twsrc%5Etfw">January 22, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## A Tale as Old as Time Itself

Or, at least, email itself.

David Knuth --- of complexity analysis & LaTeX fame --- notoriously [forswore email](https://www-cs-faculty.stanford.edu/~knuth/email.html) circa 1990.

Instead, his secretary collates messages for him to sort through, say, every six months or so.
Really.

Interestingly, in the same breath, we can all also read Knuth's Important Opinion about calling it "email" versus "e-mail."

If only we could all have such wherewithal...

## Staggered Email Delivery

Well, we can!
(Kinda.)

No mere mortal is going to get away with checking email bi-annually, but it's not too hard to to set up your Gmail inbox to only populate a few times a day.

Services like [Adios](https://adios.ai/) promise to let you to set this up in just a few clicks, but when I tried about a month ago it was running into permission issues with Google.

Instead, I [Google Scripts](https://script.google.com)-ed together a homemade solution, inspired from [here](https://www.bettercloud.com/monitor/the-academy/take-control-of-gmail-only-check-it-once-per-hour-with-google-apps-script/).

The idea is to
1. set up a Gmail filter to automatically apply a tag to incoming emails and bypass the inbox,
2. set up a regularly-scheduled job to grab all tagged emails that have piled up and move them into the inbox.

The [original source](https://www.bettercloud.com/monitor/the-academy/take-control-of-gmail-only-check-it-once-per-hour-with-google-apps-script/) has pretty good step-by-step instructions if you're interested.
Their crucial copy-paste code snippet appears to just be italicized text (containing `“` instead of `"` characters --- egad!), so here's a properly-formatted snippet for your copy-paste pleasure.

```
function processHidden() {
 var label = GmailApp.getUserLabelByName("gmail-freeze-hidden");

 if (label) {
   var threads = label.getThreads();

   for (var i = 0; i < threads.length; i++) {
     var thread = threads[i];
     thread.moveToInbox();
     thread.removeLabel(label);
   }
 }

};
```

## ListServ Pipe Dreams

How awesome would it be if our departments consolidated announcements into a weekly or daily digest instead of forwarding junk onto the listservs one-at-a-time?

Well, it turns out, *you* can set this up yourself!
It's easy to set up a separate, even-more-staggered pipeline for listserv email.

How?
You can generally tell listserv email apart from other email by checking if you're listed as a `to:` or `cc:` recipient.
Listserv email is addressed to the listserv instead of your specific email.
Then, just have the Gmail filter label listerv email with a special tag and run the job to push that tag into the inbox less often.

## Mark Archived as Read

Another regularly-scheduled I can't live without: automatically marking archived emails as read.
That way I can swipe emails out of my Gmail inbox without having to take the time to open them to prevent them from piling up as unread.
(Archiving lets you avoid permanently deleting them, too, in case you end up having to crawl back and search for them.)

Here's another Google Script snippet for your copy-paste pleasure.
Just attach it to a regularly-scheduled hook and all your archived emails will be marked read!

```
function markArchivedAsRead() {
  var threads = GmailApp.search('label:unread -label:inbox -label:gmail-freeze-hidden');
  GmailApp.markThreadsRead(threads);
};
```

## Escape from Zoom Island

My top two favorite tweets on the subject both involve clever contraptions to end virtual meetings.

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">オンライン飲み会から緊急脱出できるマシーンを作りました <a href="https://t.co/gB2Ur6f21i">pic.twitter.com/gB2Ur6f21i</a></p>&mdash; 藤原 麻里菜 | Marina Fujiwara (@togenkyoo) <a href="https://twitter.com/togenkyoo/status/1255499143147147265?ref_src=twsrc%5Etfw">April 29, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">It took some light hacking, but I now have one button to end all Zoom calls (with sound effects) <a href="https://t.co/1XXcXXPCgI">pic.twitter.com/1XXcXXPCgI</a></p>&mdash; Michael Baym (@baym) <a href="https://twitter.com/baym/status/1273307737745698816?ref_src=twsrc%5Etfw">June 17, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Zoom is the new email.
`nuff said.

## A Wireless Headset with Hardware Mute?

Univerally on blast: Zoom attendees who are not talking, but who are not on mute.
Don't be that attendee!

Zoom has a software mute feature, but this means you have to stay within reach of your Zoom device in order to be able to quickly jump into conversation.
After a week or two of all zoom all the time, I started shopping around for a wireless headset with hardware mute capabilities.

This was *surprisingly* difficult to nail down.
After spending longer than I'd care to admit aimlessly searching around, I settled on the [Logitech H800 BLUETOOTH WIRELESS HEADSET](https://www.logitech.com/en-us/product/wireless-headset-h800).

I've had mine for more than a month now and I can confirm --- the hardware mute works like a charm and is Zoom compatibile!
I am much happier for being able to hike into the kitchen to fetch fresh [Millenial Juice](https://twitter.com/daanieltran/status/950096964821114881) or even just stand up and pace around a little bit while being able to easily unmute and interject.

I found my H800 as [decent deal](https://www.ebay.com/itm/Logitech-H800-Wireless-Bluetooth-Headset-Without-Bluetooth-Receiver-IL-RT5/223973683736) used on ebay without a USB bluetooth receiver key included.

## Let's Chat

I would love to hear your thoughts on the zoom and email deluge!!
What do you do to survive?

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">new blog entitled<br><br>&quot;Life Hacks RE: Too Much Zoom &amp; Too Much Email&quot;<br><br>indubitably, the utmost critical issues of our time 🍷🧐<a href="https://t.co/Z2sXTUK7RZ">https://t.co/Z2sXTUK7RZ</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1278547301452021761?ref_src=twsrc%5Etfw">July 2, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Pop on there and drop me a line :fishing_pole_and_fish: or make a comment :raising_hand_woman:
