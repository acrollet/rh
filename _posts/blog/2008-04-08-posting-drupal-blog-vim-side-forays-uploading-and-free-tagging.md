---
layout: post
title: "Posting to a drupal blog from Vim (with side forays into uploading and free tagging)"
date: 2008-04-08 05:08:25 +0000
tags: ["drupal", "python", "xmlrpc", "vim"]
permalink: /content/posting-drupal-blog-vim-side-forays-uploading-and-free-tagging
---



So, we are finally getting closer to the long-awaited post (ha!) about
posting to drupal from vim. I've been having a lot of fun making this
plug-in suit my needs, and making it truly easy to post. Python hasn't
been too hard to learn - vim scripting is truly a weird, weird language.

Anyway, here is a (very) [rough
draft](http://reluctanthacker.rollett.org/sites/default/files/drupal_blog.vim)
of the plugin. If you want to use it, place it in your \~/.vim/plugin/
directory. You will need to apply add1sun's patch from
<http://drupal.org/node/224006> to make the blog API work basically at
all, and you'll need my patch from <http://drupal.org/node/243907> for
file/image uploads to work. Tagging isn't working quite right yet - I
made kind of a hacky patch, but I think I'm going to have to re-think
my approach and make a module for that\...

quick usage summary:

-   :ListPosts 5 will display a (extremely) minimal browser with the 5
    most recent posts. (You can modify the number of posts to suit, or
    leave it off, and it will get the 10 most recent posts)
-   :UploadImage and :UploadFile do what you would expect, with filename
    tab completion, and insert the link to the uploaded file in your
    post.
-   When you're editing your post, press :w as per usual to save it to
    Drupal.

For your viewing pleasure, a screenshot of me uploading the following
image:
![](http://reluctanthacker.rollett.org/sites/default/files/Picture%205.png)

The one frustrating thing about Vim's python integration is that it
won't display any output from python until the script has completed.
So, you're stuck wondering if anything is happening while the upload is
actually being performed\... Small price to pay, I guess!

Well, it's Time For Bed®, but I'll post more about the process of
making this plugin and what I learned along the way soon\...




