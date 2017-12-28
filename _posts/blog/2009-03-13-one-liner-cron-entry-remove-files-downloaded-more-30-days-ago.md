---
layout: post
title: "one-liner cron entry to remove files downloaded more than 30 days ago "
date: 2009-03-13 18:16:17 +0000
tags: ["shell scripting", "unix", "cron"]
permalink: /content/one-liner-cron-entry-remove-files-downloaded-more-30-days-ago
---



` 0 10 * * * /usr/bin/find ~/Downloads -ctime +30 -print0|xargs -0 rm -rf`

I assume no liability for any unintended results! ;)




