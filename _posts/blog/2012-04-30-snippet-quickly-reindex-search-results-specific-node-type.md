---
layout: post
title: "Snippet to quickly (re)index search results for a specific node type"
date: 2012-04-30 22:32:47 +0000
tags: ["drupal", "coding"]
permalink: /snippet-quickly-reindex-search-results-specific-node-type
---

Had the need to do this, saving the snippet here.

``` php
<?php

$query = db_select('node', 'n')
          ->fields('n', array('nid'))
          ->condition('type', 'content_type_machine_name', '=')
          ->execute();

while ($record = $query->fetchObject()) {
  _node_index_node($record);
}
```
