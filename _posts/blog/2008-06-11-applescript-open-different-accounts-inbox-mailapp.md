---
layout: post
title: "Applescript to open a different account\'s INBOX in Mail.app"
date: 2008-06-11 02:02:25 +0000
categories: ["mac os x", "mail.app", "applescript"]
permalink: /applescript-open-different-accounts-inbox-mailapp
---



A while ago, I threatened to post this script, and then it slipped my
mind, mostly because I switched to
[Gyazmail](http://reluctanthacker.rollett.org/node/3). At any rate, one
of the most frustrating things about Mail.app to me was having to get
out the mouse to switch between the inboxes of my various email
accounts, especially once I got [Mail
Act-On](http://www.indev.ca/MailActOn.html) working so nicely. The
applescript was harder to figure out than it perhaps should have been,
so here it is in the hopes that it will help someone.



1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    tell application [\"Mail\"]{style="color: #ff0000;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            [set]{style="color: #000000; font-weight: bold;"} the
    selected mailboxes of the front message viewer to
    [{]{style="color: #7a0874; font-weight: bold;"}mailbox
    [\"INBOX\"]{style="color: #ff0000;"} of account
    [\"Gmail\"]{style="color: #ff0000;"}[}]{style="color: #7a0874; font-weight: bold;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            delay [0.1]{style="color: #000000;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            [set]{style="color: #000000; font-weight: bold;"}
    no\_selected to get count selection
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    end tell
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [if]{style="color: #000000; font-weight: bold;"}
    [(]{style="color: #7a0874; font-weight: bold;"}no\_selected is equal
    to
    [0]{style="color: #000000;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [then]{style="color: #000000; font-weight: bold;"}
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            tell application [\"System
    Events\"]{style="color: #ff0000;"}
    :::

9.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
                    [set]{style="color: #000000; font-weight: bold;"}
    selected of row [-1]{style="color: #660033;"} of table
    [1]{style="color: #000000;"} of scroll area
    [1]{style="color: #000000;"} of splitter group
    [2]{style="color: #000000;"} of window [1]{style="color: #000000;"}
    of application process [\"Mail\"]{style="color: #ff0000;"} to
    [true]{style="color: #c20cb9; font-weight: bold;"}
    :::

10. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            end tell
    :::

11. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    end [if]{style="color: #000000; font-weight: bold;"}
    :::



Paste the script into Script Editor.app, change Gmail to whatever you
have your account named, and save it to \~/Library/Scripts. You\'ll need
to use something like [Quicksilver](http://www.blacktree.com/) or
[FastScripts](http://www.red-sweater.com/fastscripts/index.html) to set
up a keyboard shortcut, and then away you go.




