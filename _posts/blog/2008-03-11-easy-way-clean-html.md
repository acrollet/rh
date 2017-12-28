---
layout: post
title: "easy way to clean up html"
date: 2008-03-11 02:37:01 +0000
tags: ["html", "perl", "bash", "shell scripting"]
permalink: /easy-way-clean-html
---



While I was working on a website migration for work, I found myself
wanting a way to preserve formatting without keeping really poorly
formatted html. (probably made by Word, a lot of blockquotes instead of
list tags, etc.)

Anyway, I had good luck running the files through links (or lynx) -dump,
and then using [txt2html](http://txt2html.sourceforge.net/) to
re-htmlize them. Produced nice clean, well-formatted html. I still had
to strip out the titles with sed, but this made a quick way of doing a
clean job on lots of files with a minimum of effort.




