---
layout: post
title: "Effective Pair Programming: Line numbers"
date: 2012-09-14 12:48
comments: true
categories:
  - pair programming
---

This isn’t one of the obvious things to configure when you’re new to pair programming - but having line numbers turned on in your editor makes communicating go much more smoothly.

As the driver in the pair, it’s significantly less effort for you to jump to a line number than it is for you to mentally parse code outside your immediate mental scope.
And any respectable editor has keyboard shortcuts to jump to a specific line ([in Vim](http://vim.wikia.com/wiki/Go_to_line), I prefer to use `:42`).

As the non-driver in the pair, if I notice a line with an extra double quote, for instance, it’s easier to me to say "there’s an extra quote on line 42" than it is for me to tell you "look at the second time you called the `helper` function inside the `render` call".
I don’t have to do any mental gymnastics to verbally describe the line in question, and neither do you to understand where I want you to look.

Another great advantage of using line numbers is that there's fewer reasons for people to point at (and inevitably smudge) your display.

Be an effective pair. Use line numbers.
