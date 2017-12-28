---
layout: post
title: "miscellaneous shell-fu"
date: 2009-02-24 04:31:26 +0000
categories: ["bash", "shell scripting"]
permalink: /content/miscellaneous-shell-fu
---



Not too much to share today - just a couple neat little things I ran
across over the past couple of days, to wit:

1\. if you give chown a user with a trailing colon, it will automatically
use that user\'s default group. ex:\



1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"mailto:root@rollett\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}root[@]{style="color: #000000; font-weight: bold;"}rollett[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"}:\~[/]{style="color: #000000; font-weight: bold;"}blog[\#
    touch t]{style="color: #666666; font-style: italic;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"mailto:root@rollett\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}root[@]{style="color: #000000; font-weight: bold;"}rollett[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"}:\~[/]{style="color: #000000; font-weight: bold;"}blog[\#
    ls -l t]{style="color: #666666; font-style: italic;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [-rw-r\--r\--]{style="color: #660033;"} [1]{style="color: #000000;"}
    root root [0]{style="color: #000000;"} Feb
    [23]{style="color: #000000;"}
    [22]{style="color: #000000;"}:[21]{style="color: #000000;"} t
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"mailto:root@rollett\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}root[@]{style="color: #000000; font-weight: bold;"}rollett[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"}:\~[/]{style="color: #000000; font-weight: bold;"}blog[\#
    chown www-data: t]{style="color: #666666; font-style: italic;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"mailto:root@rollett\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}root[@]{style="color: #000000; font-weight: bold;"}rollett[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"}:\~[/]{style="color: #000000; font-weight: bold;"}blog[\#
    ls -l t]{style="color: #666666; font-style: italic;"}
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [-rw-r\--r\--]{style="color: #660033;"} [1]{style="color: #000000;"}
    www-data www-data [0]{style="color: #000000;"} Feb
    [23]{style="color: #000000;"}
    [22]{style="color: #000000;"}:[21]{style="color: #000000;"} t
    :::



2\. [Pinfo](http://pinfo.sourceforge.net/) is a more user-friendly [info
file](http://www.gnu.org/software/texinfo/) reader/browser. The jk keys
do what any God-fearing vi user would expect them to.

@rant: I don\'t want to learn emacs keystrokes just to read info that
should have been in the man page! durn kids these days\...

that\'s all for today!




