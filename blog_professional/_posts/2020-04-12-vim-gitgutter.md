---
layout: post
title:  "Overoptimized vim-gitgutter Config"
date:   2020-04-12
no_toc: true
---

I spent a lot of this last weekend aspirationally re-upping my vim game.
That's what there is to do for fun nowadays, I guess.
Maybe I'll actually stick to it this time.

Characteristically, I spent too long fiddling with things that don't matter.
In particular, I really tweaked out over git diff symbols in the gutter.

I felt that the the default `+` and `-` symbols don't efficiently show the
spatial structure of the diffs they represented.
I addressed this by using full-width underscore elements for the deletion diffs (where the deleted lines are just below) and a mirrored L shape for the deletion plus modification diffs (representing changes to the current line in addition to deletion below).

I also felt the diff symbols lacked visual weight necessary to make their color coding pop.
I fixed this by prepending the diff symbols with a full-character box.

Anyways, I spent long enough combing through the ASCII character set and playing
with different options figured it might be worth a share.
Here's a screen grab example of the gutter diff symbols I eventually settled on in action.

![The gutter symbols in action.](/resources/vim-gitgutter-example.jpg){:width="100%"}

Here's the relevant `.vimrc` bits for your copy/paste pleasure.

```
let g:gitgutter_sign_added = '█|'
let g:gitgutter_sign_modified = '█⫶'
let g:gitgutter_sign_removed = '█▁'
let g:gitgutter_sign_removed_first_line = '█▔'
let g:gitgutter_sign_modified_removed = "█▟"
```

## Let's Chat

I would love to hear your thoughts, questions, and comments RE: the joys of
.vimrc!

I started a twitter thread (right below) so we can chat :phone: :phone: :phone:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">new mini blog post entitled<br><br>&quot;Over-optimized vim-gitgutter Config&quot;<br><br>yeah so I guess that&#39;s what I&#39;m up to for fun these days 🤷<ahref="https://t.co/qnXDyd0X4g">https://t.co/qnXDyd0X4g</a><br><br>very proud of my top notch emoji movie example text at least smh <a href="https://t.co/1FrNNlnJf4">pic.twitter.com/1FrNNlnJf4</a></p>&mdash; mmore500 (@mmore500) <a href="https://twitter.com/mmore500/status/1249544580174729217?ref_src=twsrc%5Etfw">April 13, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
