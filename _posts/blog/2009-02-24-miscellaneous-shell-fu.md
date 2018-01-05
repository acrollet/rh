---
layout: post
title: "miscellaneous shell-fu"
date: 2009-02-24 04:31:26 +0000
tags: ["bash", "shell scripting"]
permalink: /content/miscellaneous-shell-fu
---

Not too much to share today - just a couple neat little things I ran
across over the past couple of days, to wit:

if you give chown a user with a trailing colon, it will automatically
use that user's default group. ex:

``` sh
root@rollett:~/blog# touch t
root@rollett:~/blog# ls -l t
-rw-r--r-- 1 root root 0 Feb 23 22:21 t
root@rollett:~/blog# chown www-data: t
root@rollett:~/blog# ls -l t
-rw-r--r-- 1 www-data www-data 0 Feb 23 22:21 t
```

[Pinfo](http://pinfo.sourceforge.net/) is a more user-friendly [info
file](http://www.gnu.org/software/texinfo/) reader/browser. The jk keys
do what any God-fearing vi user would expect them to.

@rant: I don't want to learn emacs keystrokes just to read info that
should have been in the man page! durn kids these days...

that's all for today!
