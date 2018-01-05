---
layout: post
title: "Editing python with Vim"
date: 2009-02-22 04:38:28 +0000
tags: ["python", "vim", "coding"]
permalink: /content/editing-python-vim
---



Found a nice post on this kind of stuff
[here.](http://blog.sontek.net/2008/05/11/python-with-a-modular-ide-vim/)
I haven't implemented all of it by any means, but the omnifunc code
completion and
[snippetsEmu](http://www.vim.org/scripts/script.php?script_id=1318) are
quite nice. Also did my own hacky perversion of the :make command.
.vimrc excerpt follows\...

``` viml
" py stuff
autocmd BufRead *.py set smartindent cinwords=if,elif,else,for,while,try,except,finally,def,class
autocmd FileType python set omnifunc=pythoncomplete#Complete
autocmd FileType python set makeprg=python\ %
```
