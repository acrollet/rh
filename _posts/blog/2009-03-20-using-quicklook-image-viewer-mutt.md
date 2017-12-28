---
layout: post
title: "Using quicklook as an image viewer for mutt"
date: 2009-03-20 02:53:02 +0000
categories: ["mac os x", "mutt", "email", "imap"]
permalink: /content/using-quicklook-image-viewer-mutt
---

So, I\'m wavering between email clients yet again - giving the
[mutt](http://www.mutt.org/)+[isync](http://isync.sourceforge.net/)
combination a try this time\... Mutt\'s disconnected imap support is
sadly lacking, and I\'ve messed with
[offlineimap](http://software.complete.org/software/projects/show/offlineimap)
before, but found it a bit too fiddly. Anyway, I thought quicklook would
be a nice way to view the many highly important images I often get in my
email, as it pops up quickly, and doesn\'t require an application
switch. A quick google scared up the \'qlmanage\' utility, and I wrote a
quick wrapper script to provide mutt with a 0 exit status instead of the
130 that qlmanage spits out. (ummm, whatever, apple) This prevents mutt
from spitting out the \'press any key to continue\' message and
requiring an EXTRA KEYSTROKE. (picky, picky\...)

``` bash
#!/bin/bash
QLFILE=$1
 
# we have to trap ctrl-c so that a successful exit signal will be given,
# so that mutt won't prompt us to press any key to continue
trap 'exit 0' 2 #traps Ctrl-C (signal 2)
 
qlmanage -p $QLFILE >& /dev/null
```


A little adjustment in \~/.mailcap, and away you go\... Here\'s an
example of one of the very important images that it\'s vital I see in my
email:
![](http://reluctanthacker.rollett.org/sites/default/files/Picture35.png)

