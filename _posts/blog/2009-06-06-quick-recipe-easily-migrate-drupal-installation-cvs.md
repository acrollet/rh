---
layout: post
title: "Quick recipe to easily migrate a drupal installation to CVS"
date: 2009-06-06 23:15:46 +0000
categories: ["drupal", "bash", "drush", "cvs"]
permalink: /content/quick-recipe-easily-migrate-drupal-installation-cvs
---



I recently had to update a number of drupal installations, some of them
quite old. Here is a bash \"few-liner\" to migrate an install to CVS,
making it much easier to update in the future.

``  cd your_drupal_dir # replace DRUPAL-6-12 with the appropriate version tag cvs -z6 -d :pserver:anonymous:anonymous@cvs.drupal.org:/cvs/drupal checkout  \ -r DRUPAL-6-12 new_drupal rm -rf new_drupal/sites mkdir old_drupal for i in `ls drupal`; do mv $i old_drupal; mv drupal/$i .; done # if you have drush drush updatedb # make sure everything's working, then rm -rf old_drupal ``

Standard disclaimers apply, hope this helps some people!




