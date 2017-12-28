---
layout: post
title: "Creating a regex for finding credit card numbers with grep"
date: 2008-04-18 20:33:44 +0000
tags: []
permalink: /creating-regex-finding-credit-card-numbers-grep
---



Ugly regex:

    grep '\(^\|[^0-9]\)\{1\}\([345]\{1\}[0-9]\{3\}\|6011\)\{1\}[-]\?[0-9]\{4\}[-]\?\
           [0-9]\{2\}[-]\?[0-9]\{2\}-\?[0-9]\{1,4\}\($\|[^0-9]\)\{1\}' filename

Lately, I\'ve been working with the security team where I\'m employed to
catch people storing information they shouldn\'t be on our database
server. (SSNs, credit card numbers, etc.) This involved dumping all our
databases into a flat file (about a gig of text) and doing some mining.
I was given a pre-built regex, but it didn\'t work with grep, I\'m
enough of a command-line geek that I\'d rather do things \'my way\' than
just write a perl script or something. So, I had to make my own regex to
find cc numbers, because I didn\'t find anything effective in a quick
search online. This brings to mind a hoary old chestnut of a quote -
over-used, but still very true:

    Some people, when confronted with a problem, think "I know, I'll use regular expressions." 
    Now they have two problems. 

    -Jamie Zawinski, in comp.lang.emacs

All that notwithstanding, I found a few resources that came in handy for
this project.

-   [This php
    tutorial](http://www.sitepoint.com/article/card-validation-class-php)
    has a very good description of a basic spec for valid cc numbers.
-   [This page](http://credit-card-information.elliottback.com/) has
    more info on valid numbers, and test numbers for all the major
    companies.
-   [Txt2regex](http://txt2regex.sourceforge.net/) is a handy
    command-line utility that will ask for information on what you want
    to match, and build regexes of many different formats step-by-step.
    It didn\'t do everything for me, but it can be a handy way to get
    close to what you want without having to dive into the man pages\...
-   [Handy article on gnu grep](http://www.linux.com/articles/54514)
    from linux.com - more info just below.

Once you think you\'ve got your regex built, gnu grep has some options
not available in standard versions of grep that are very handy for
debugging. The -o switch will output only the matched part of the
string, ex:

![](http://reluctanthacker.rollett.org/sites/default/files/Picture%2011.png)

The \--color switch will highlight matches - very handy when you\'re
searching through dense SQL dumps!

![](http://reluctanthacker.rollett.org/sites/default/files/Picture%2010.png)




