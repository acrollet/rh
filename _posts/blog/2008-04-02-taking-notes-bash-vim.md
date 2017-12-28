---
layout: post
title: "taking notes with bash + vim"
date: 2008-04-02 02:55:45 +0000
categories: ["bash", "note", "vim"]
permalink: /content/taking-notes-bash-vim
---



A co-worker sold me on the utility of having a program like
[Yojimbo](http://www.barebones.com/products/yojimbo/). However, I\'m too
cheap to shell out the \$39 for a license, and I prefer to have vi key
bindings, and complete keyboard control. I found an excellent post at
[make-believe.org](http://www.make-believe.org/in-words/post/bashing-out-notes)
which describes a system for note-taking using a little bash magic for
searching and command line tab completion, and vim for editing. I liked
it a lot, but decided to add tagging to the system. Read on to find out
how I did it.

    host:~ $ note testnote

![](http://reluctanthacker.rollett.org/sites/default/files/images/Picture%2012.png)

(:xa will save all buffers and quit in one swell foop)

    host:~ $ findnote note
    /Users/acrollet/.notes/test note.note
    1:This is a test note.

    host:~ $ findtag bash
    /Users/acrollet/.notes/test note.tags
    1:bash vi note-taking

The bash file to do the above looks like this:


``` bash
note() {
  if [ -n "$*" ]; then
    mvim -o2 "$HOME/.notes/$*.note" "$HOME/.notes/$*.tags"
  else
    printf "Name of note is a required argument.\n"
  fi
}
 
findnote() {
  ack -ia $1 ~/.notes/*.note
}
 
shownote() {
  cat "$HOME/.notes/$*.note"
}
 
findtag() {
  ack -ia $1 ~/.notes/*.tags
}
 
copynote() {
  cat "$HOME/.notes/$*.note" | pbcopy
}
 
alias note:='note'
alias shownote:='shownote'
alias notes="mvim -c \"let g:netrw_list_hide='\.tags$,^\..*'\" -c \"let g:netrw_hide=1\" $HOME/.notes"
 
_notes() {
  local cur names IFS
 
  cur="${COMP_WORDS[COMP_CWORD]}"
  names=`ls $HOME/.notes | sed 's/.note$//g'`
  IFS=$'\t\n'
 
  COMPREPLY=( $(compgen -W "${names}" -- ${cur}) )
  return 0
}
complete -o nospace -F _notes note
complete -o nospace -F _notes note:
complete -o nospace -F _notes copynote
```


Now, here\'s the other piece. Put this in your .vimrc:

    let g:netrw_hide=1
    let g:netrw_list_hide='\.tags$,^\..*'

And this in
[netrwFileHandlers.vim](http://www.vim.org/scripts/script.php?script_id=1075):
(you may need a more recent version than came with your distribution,
v98 did not work for me)

    " ---------------------------------------------------------------------
    "
    " s:NFH_note: handles note file when the user hits "x" when the \{\{\{1
    "                        cursor is atop a *.note file
    fun! s:NFH_note(notefile)
    "  call Dfunc("s:NFH_note(".a:notefile.")")

      let note= substitute(a:notefile,'\ ','\\\ ','g')
      let tags= substitute(a:notefile,'\.note$','\.tags','')
      let tag= substitute(tags,'\ ','\\\ ','g')

       " call Decho("opening "page)
       execute "e "tag
       execute "sp "note
       return 0
    endfun

Now, when you type \'notes\' at the prompt, you\'ll get this view:

![](http://reluctanthacker.rollett.org/sites/default/files/images/Picture%2013.preview.png)\
\
Place the cursor over the note you wish to edit, press \'x\', and it
will open up the split-pane view with the note and tag files. I welcome
suggestions for improvements!




