---
layout: post
title: "Editing python with Vim"
date: 2009-02-22 04:38:28 +0000
categories: ["python", "vim", "coding"]
permalink: /content/editing-python-vim
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
Found a nice post on this kind of stuff
[here.](http://blog.sontek.net/2008/05/11/python-with-a-modular-ide-vim/)
I haven\'t implemented all of it by any means, but the omnifunc code
completion and
[snippetsEmu](http://www.vim.org/scripts/script.php?script_id=1318) are
quite nice. Also did my own hacky perversion of the :make command.
.vimrc excerpt follows\...

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\" py stuff]{style="color: #ff0000;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [autocmd BufRead \*.py set smartindent
    cinwords=if,elif,else,for,while,try,except,finally,def,class
     ]{style="color: #ff0000;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [autocmd FileType python set
    omnifunc=pythoncomplete\#Complete]{style="color: #ff0000;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [autocmd FileType python set makeprg=python\\ %
    ]{style="color: #ff0000;"}
    :::
:::
:::
:::
:::
:::

