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



1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    note[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [if]{style="color: #000000; font-weight: bold;"}
    [\[]{style="color: #7a0874; font-weight: bold;"}
    [-n]{style="color: #660033;"} [\"\$\*\"]{style="color: #ff0000;"}
    [\]]{style="color: #7a0874; font-weight: bold;"};
    [then]{style="color: #000000; font-weight: bold;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        mvim [-o2]{style="color: #660033;"}
    [\"[\$HOME]{style="color: #007800;"}/.notes/\$\*.note\"]{style="color: #ff0000;"}
    [\"[\$HOME]{style="color: #007800;"}/.notes/\$\*.tags\"]{style="color: #ff0000;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [else]{style="color: #000000; font-weight: bold;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        [printf]{style="color: #7a0874; font-weight: bold;"} [\"Name of
    note is a required
    argument.[\\n]{style="color: #000099; font-weight: bold;"}\"]{style="color: #ff0000;"}
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [fi]{style="color: #000000; font-weight: bold;"}
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

9.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    findnote[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

10. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      ack [-ia]{style="color: #660033;"} [\$1]{style="color: #007800;"}
    \~[/]{style="color: #000000; font-weight: bold;"}.notes[/\*]{style="color: #000000; font-weight: bold;"}.note
    :::

11. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

12. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

13. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    shownote[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

14. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [cat]{style="color: #c20cb9; font-weight: bold;"}
    [\"[\$HOME]{style="color: #007800;"}/.notes/\$\*.note\"]{style="color: #ff0000;"}
    :::

15. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

16. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

17. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    findtag[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

18. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      ack [-ia]{style="color: #660033;"} [\$1]{style="color: #007800;"}
    \~[/]{style="color: #000000; font-weight: bold;"}.notes[/\*]{style="color: #000000; font-weight: bold;"}.tags
    :::

19. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

20. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

21. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    copynote[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

22. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [cat]{style="color: #c20cb9; font-weight: bold;"}
    [\"[\$HOME]{style="color: #007800;"}/.notes/\$\*.note\"]{style="color: #ff0000;"}
    [\|]{style="color: #000000; font-weight: bold;"} pbcopy
    :::

23. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

24. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

25. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [alias]{style="color: #7a0874; font-weight: bold;"}
    note:=[\'note\']{style="color: #ff0000;"}
    :::

26. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [alias]{style="color: #7a0874; font-weight: bold;"}
    shownote:=[\'shownote\']{style="color: #ff0000;"}
    :::

27. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [alias]{style="color: #7a0874; font-weight: bold;"}
    [notes]{style="color: #007800;"}=[\"mvim -c
    [\\\"]{style="color: #000099; font-weight: bold;"}let
    g:netrw\_list\_hide=\'\\.tags\$,\^\\..\*\'[\\\"]{style="color: #000099; font-weight: bold;"}
    -c [\\\"]{style="color: #000099; font-weight: bold;"}let
    g:netrw\_hide=1[\\\"]{style="color: #000099; font-weight: bold;"}
    [\$HOME]{style="color: #007800;"}/.notes\"]{style="color: #ff0000;"}
    :::

28. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

29. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    \_notes[(]{style="color: #7a0874; font-weight: bold;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [{]{style="color: #7a0874; font-weight: bold;"}
    :::

30. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [local]{style="color: #7a0874; font-weight: bold;"} cur names IFS
    :::

31. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

32. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [cur]{style="color: #007800;"}=[\"[\${COMP\_WORDS\[COMP\_CWORD\]}]{style="color: #007800;"}\"]{style="color: #ff0000;"}
    :::

33. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [names]{style="color: #007800;"}=[\`]{style="color: #000000; font-weight: bold;"}[ls]{style="color: #c20cb9; font-weight: bold;"}
    [\$HOME]{style="color: #007800;"}[/]{style="color: #000000; font-weight: bold;"}.notes
    [\|]{style="color: #000000; font-weight: bold;"}
    [sed]{style="color: #c20cb9; font-weight: bold;"}
    [\'s/.note\$//g\']{style="color: #ff0000;"}[\`]{style="color: #000000; font-weight: bold;"}
    :::

34. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [IFS]{style="color: #007800;"}=\$[\'\\t\\n\']{style="color: #ff0000;"}
    :::

35. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

36. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [COMPREPLY]{style="color: #007800;"}=[(]{style="color: #7a0874; font-weight: bold;"}
    \$[(]{style="color: #7a0874; font-weight: bold;"}[compgen]{style="color: #7a0874; font-weight: bold;"}
    [-W]{style="color: #660033;"}
    [\"[\${names}]{style="color: #007800;"}\"]{style="color: #ff0000;"}
    [\--]{style="color: #660033;"}
    [\${cur}]{style="color: #800000;"}[)]{style="color: #7a0874; font-weight: bold;"}
    [)]{style="color: #7a0874; font-weight: bold;"}
    :::

37. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
      [return]{style="color: #7a0874; font-weight: bold;"}
    [0]{style="color: #000000;"}
    :::

38. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

39. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [complete]{style="color: #7a0874; font-weight: bold;"}
    [-o]{style="color: #660033;"} nospace [-F]{style="color: #660033;"}
    \_notes note
    :::

40. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [complete]{style="color: #7a0874; font-weight: bold;"}
    [-o]{style="color: #660033;"} nospace [-F]{style="color: #660033;"}
    \_notes note:
    :::

41. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [complete]{style="color: #7a0874; font-weight: bold;"}
    [-o]{style="color: #660033;"} nospace [-F]{style="color: #660033;"}
    \_notes copynote
    :::



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




