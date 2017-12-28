---
layout: post
title: "Snippet to quickly (re)index search results for a specific node type"
date: 2012-04-30 22:32:47 +0000
categories: ["drupal", "coding"]
permalink: /snippet-quickly-reindex-search-results-specific-node-type
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
Had the need to do this, saving the snippet here.

::: {.geshifilter}
::: {.php .geshifilter-php style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\<?php]{style="color: #000000; font-weight: bold;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\$query]{style="color: #000088;"}[=]{style="color: #339933;"}
    db\_select[(]{style="color: #009900;"}[\'node\']{style="color: #0000ff;"}[,]{style="color: #339933;"}
    [\'n\']{style="color: #0000ff;"}[)]{style="color: #009900;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [-\>]{style="color: #339933;"}[fields]{style="color: #004000;"}[(]{style="color: #009900;"}[\'n\']{style="color: #0000ff;"}[,]{style="color: #339933;"}
    [[array]{style="color: #990000;"}](http://www.php.net/array)[(]{style="color: #009900;"}[\'nid\']{style="color: #0000ff;"}[)]{style="color: #009900;"}[)]{style="color: #009900;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [-\>]{style="color: #339933;"}[condition]{style="color: #004000;"}[(]{style="color: #009900;"}[\'type\']{style="color: #0000ff;"}[,]{style="color: #339933;"}
    [\'content\_type\_machine\_name\']{style="color: #0000ff;"}[,]{style="color: #339933;"}
    [\'=\']{style="color: #0000ff;"}[)]{style="color: #009900;"}
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    [-\>]{style="color: #339933;"}[execute]{style="color: #004000;"}[(]{style="color: #009900;"}[)]{style="color: #009900;"}[;]{style="color: #339933;"}
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [while]{style="color: #b1b100;"}
    [(]{style="color: #009900;"}[\$record]{style="color: #000088;"}
    [=]{style="color: #339933;"}
    [\$query]{style="color: #000088;"}[-\>]{style="color: #339933;"}[fetchObject]{style="color: #004000;"}[(]{style="color: #009900;"}[)]{style="color: #009900;"}[)]{style="color: #009900;"}
    [{]{style="color: #009900;"}
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    \_node\_index\_node[(]{style="color: #009900;"}[\$record]{style="color: #000088;"}[)]{style="color: #009900;"}[;]{style="color: #339933;"}
    :::

9.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #009900;"}
    :::
:::
:::
:::
:::
:::

