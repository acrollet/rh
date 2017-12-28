---
layout: post
title: "Full integration of mutt and the OS X Addressbook"
date: 2009-03-23 03:51:34 +0000
categories: ["mac os x", "applescript", "mutt", "email", "imap", "addressbook", "lbdb"]
permalink: /content/full-integration-mutt-and-os-x-addressbook
---


http://reluctanthacker.rollett.org/sites/default/files/sites/default/files/add\_address.sh\_.txt


So, my experiments with mutt continue. Incidentally, if you think that
I\'m crazy for using a cli email client in this day and age\... Well,
you\'re probably right. However, I\'m crazy, but not alone, as the
dearth of great email clients for Mac OS X is something that\'s been
[written about a lot](http://mronge.com/2007/07/06/the-state-of-email/).
Anyway, that\'s a short way of saying that I think that mutt+\"a whole
bunch of utilities to add functionality to it\" is a (at least somewhat)
reasonable solution, given the alternatives.\
\

Anyway, [linsec.ca](http://linsec.ca/Using_mutt_on_OS_X) has probably
the most info there is in one place on integrating mutt with OS X. I
really like that lbdb gives me the capability to search the OS X
addressbook, but I also wanted to the ability to add addresses directly
from mutt. A little bit of dirty hackery with bash and osascript later,
I have a working solution. This script assumes a working lbdb install,
but beyond that, all you need to do is add the following line to your
\~/.muttrc and place the attached script in your \~/bin directory. Then,
press \'A\' on any message in mutt. The script will search for an
existing record with the same name, and add the address to that, or
create a new record if necessary. You will also be prompted to pick a
label from those currently in use in your addressbook.

``` bash
macro index,pager A "<pipe-message>/opt/local/bin/lbdb-fetchaddr -x from -d ''<return><shell-escape>$HOME/bin/add_address.sh<return>" "add the sender address to os x addressbook"
```
