---
layout: post
title: "Copy/paste Magic to Untruncate Filenames on GitHub"
date: 2021-06-03
no_toc: true
---

Not quite a full blog post, but a usefull tidbit nonetheless.

Open up developer view (`ctrl-I`, usually) and paste this into your JavaScript console to untruncate long filenames on GitHub's tree view.

```javascript
var targets = document.getElementsByClassName("css-truncate");
while (targets.length)
    targets[0].className = targets[0].className.replace(/\bcss-truncate\b/g, "");
```

Adapted from [here](https://stackoverflow.com/a/26362454).
