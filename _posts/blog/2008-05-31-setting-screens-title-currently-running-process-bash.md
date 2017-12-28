---
layout: post
title: "Setting Screen\'s title to the currently running process with bash"
date: 2008-05-31 16:49:54 +0000
categories: ["bash", "screen", "gnu screen", "shell scripting", "system administration"]
permalink: /setting-screens-title-currently-running-process-bash
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
This is the first of a series of at least two posts about how I\'ve
configured the excellent [Gnu
Screen](http://www.gnu.org/software/screen/) to fit my needs and make me
more productive.

My workflow tends to be fairly disjointed, simply because I tend to do a
mix of system administration and programming, with user requests
scattered through the day. I decided to start using screen at work
because I was having a number of connection dropouts, and having to
start from scratch quite often. It\'s important for me to have a visual
cue of what\'s going on in each virtual terminal, as I\'ll often have 6
or 7 or more tasks going at once. Given that I\'m not bloody likely to
manually change the title each time I start a task, I needed a way to
automatically do so. [This page](http://aperiodic.net/screen/titles)
from the excellent screen faq on
[aperiodic.net](http://www.aperiodic.net/screen/) has instructions that
tell you how to use a clever combination of the shelltitle screen
configuration and a bash prompt setting to let you set the title to the
current running process. However, this just gives the process name, and
not arguments - so, I would have three shells titled \'vi\', and another
four titled \'ssh\'. Not so much use, not knowing what I\'m editing, or
what hosts I\'m logged onto. Unfortunately, bash doesn\'t have a
preexec() built-in like zsh does. I suppose that I could switch to zsh,
but I\'m ornery.

However, I did find an excellent post on
[davidpashley.com](http://www.davidpashley.com/articles/xterm-titles-with-bash.html)
that gave me the key. An extremely clever use of a trap will let you
emulate zsh\'s preexec function and run whatever you like just before
each command is executed. Here\'s how I modified his code:

    case "$TERM" in
      screen)
          set -o functrace
          trap 'echo -ne "\ek\$:${BASH_COMMAND:0:20}\e\\"' DEBUG
          export PS1='\[\033k$:\W\033\\\]\u@\h:\w\$ '
        ;;
      *)
        ;;
    esac

Finally, here\'s the obligatory screenshot.

![](http://reluctanthacker.rollett.org/sites/default/files/Picture%2013.png)
:::
:::
:::

