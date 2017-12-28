---
layout: post
title: "Drupal BlogAPI client - new version"
date: 2009-01-27 22:31:13 +0000
categories: ["drupal", "xmlrpc", "vim", "blogapi"]
permalink: /drupal-blogapi-client-new-version
---



http://reluctanthacker.rollett.org/sites/default/files/sites/default/files/drupal\_blog.vim\_.sanitized




Thanks to a
[suggestion](http://reluctanthacker.rollett.org/node/39#comment-15) on
an earlier post, I decided to extend the infamous VIM blogging client to
all content types. It now comes with the capability to edit pages and
stories by default, and it\'s easily extendible to other content types.
(though you\'re restricted to editing the title and body, it won\'t do
custom fields!) I suppose this would make the version number something
like 0.03-rc2? Here\'s the (by now) de rigeur screenshot:

![](http://reluctanthacker.rollett.org/sites/default/files/Picture%2030_1.png)

You\'ll need to apply my patch from <http://drupal.org/node/243907> to
make file/image uploads work.

To use it, just download the file below, edit it to add your username,
password, and URL, and place it in \~/.vim/plugin. (or wherever else you
prefer)

Please leave a comment if you end up using this - it\'s really the only
thing that encourages me to continue development!







