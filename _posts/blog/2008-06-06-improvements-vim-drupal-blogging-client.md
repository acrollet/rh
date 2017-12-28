---
layout: post
title: "Improvements to the Vim drupal blogging client "
date: 2008-06-06 14:33:58 +0000
tags: ["drupal", "python", "xmlrpc", "vim"]
permalink: /improvements-vim-drupal-blogging-client
---



I\'ve made a few improvements to my Drupal blogging client, first spoken
about [here](http://reluctanthacker.rollett.org/node/25). It now has the
ability to publish and unpublish posts, delete posts, and create and
edit free tags (folksonomy). The free tagging feature requires a module
that I\'ve packaged up for parsing tags in the post body - just waiting
on permission from the author of the sample code I modified before
posting that. Hopefully it\'ll be coming soon!

![](http://reluctanthacker.rollett.org/sites/default/files/Picture%2020.png)

There are two new commands - :PublishPost and :SavePost. (:w still
publishes a post, as before) Unfortunately, the drupal blogapi does not
expose whether a post is published or not, so I had to resort to
modifying the post title to show the post status. Hacky, but it works!

I ran across a couple of very nice tools for working with xmlrpc while I
was trying to get this all to work. First off is a great little tool
called [XML-RPC Client](http://ditchnet.org/xmlrpc/) - it\'s just a Mac
Os X (Cocoa) tool that lets you make an xmlrpc call, view the generated
xml, and view the returned results as xml and a struct.

Second, I found this [proxy
script](http://www.myelin.co.nz/notes/xmlrpc-debug-proxy.html) written
in python - it made debugging much, much easier\...

Without further ado, here is the newest version of
[drupal\_blog.vim](http://reluctanthacker.rollett.org/sites/default/files/drupal_blog.vim.sanitized).
As before, you will need to apply add1sun\'s patch from
<http://drupal.org/node/224006> to make the blog API work basically at
all, and you\'ll need my patch from <http://drupal.org/node/243907> for
file/image uploads to work.




