---
layout: post
title: "Using quicklook as an image viewer for mutt"
date: 2009-03-20 02:53:02 +0000
categories: ["mac os x", "mutt", "email", "imap"]
permalink: /content/using-quicklook-image-viewer-mutt
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
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

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\#!/bin/bash]{style="color: #666666; font-style: italic;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [QLFILE]{style="color: #007800;"}=[\$1]{style="color: #007800;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# we have to trap ctrl-c so that a successful exit signal will be
    given,]{style="color: #666666; font-style: italic;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# so that mutt won\'t prompt us to press any key to
    continue]{style="color: #666666; font-style: italic;"}
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [trap]{style="color: #7a0874; font-weight: bold;"} [\'exit
    0\']{style="color: #ff0000;"} [2]{style="color: #000000;"} [\#traps
    Ctrl-C (signal 2)]{style="color: #666666; font-style: italic;"}
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    qlmanage [-p]{style="color: #660033;"}
    [\$QLFILE]{style="color: #007800;"}
    [\>&]{style="color: #000000; font-weight: bold;"}
    [/]{style="color: #000000; font-weight: bold;"}dev[/]{style="color: #000000; font-weight: bold;"}null
    :::
:::
:::

A little adjustment in \~/.mailcap, and away you go\... Here\'s an
example of one of the very important images that it\'s vital I see in my
email:
![](http://reluctanthacker.rollett.org/sites/default/files/Picture35.png)
:::
:::
:::

