---
layout: post
title: "Applescript to open a different account's INBOX in Mail.app"
date: 2008-06-11 02:02:25 +0000
tags: ["mac os x", "mail.app", "applescript"]
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


``` applescript
tell application "Mail"
        set the selected mailboxes of the front message viewer to {mailbox "INBOX" of account "Gmail"}
        delay 0.1
        set no_selected to get count selection
end tell
 
if (no_selected is equal to 0) then
        tell application "System Events"
                set selected of row -1 of table 1 of scroll area 1 of splitter group 2 of window 1 of application process "Mail" to true
        end tell
end if
```


Paste the script into Script Editor.app, change Gmail to whatever you
have your account named, and save it to \~/Library/Scripts. You'll need
to use something like [Quicksilver](http://www.blacktree.com/) or
[FastScripts](http://www.red-sweater.com/fastscripts/index.html) to set
up a keyboard shortcut, and then away you go.




