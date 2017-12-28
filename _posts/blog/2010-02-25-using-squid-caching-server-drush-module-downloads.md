---
layout: post
title: "Using squid as a caching server for drush module downloads"
date: 2010-02-25 18:07:36 +0000
categories: ["drupal", "drush", "proxy"]
permalink: /using-squid-caching-server-drush-module-downloads
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
Intro
-----

Due to [popular request](http://drupal.org/node/698104#comment-2645318),
I\'ve decided to quickly document how we at [UNT Web
support](https://webadmin.unt.edu) use
[squid](http://www.squid-cache.org/) as a proxy caching server for
[drush](http://drupal.org/project/drush). The main goal was to speed up
module updates, and reduce the load on drupal.org and UNT\'s internet
connection. The instructions are based on my memory, and are for
[Debian](http://debian.org), so there may be gaps here and there
depending on your experience/OS.

Squid Setup
-----------

Installation was super-simple. (gotta love apt)

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [apt-get install]{style="color: #c20cb9; font-weight: bold;"} squid3
    :::
:::
:::

Configuration was also quite simple. Basically, the debian package for
squid is setup fairly nicely as a proxy caching server out of the box,
and you need only configure access. First, add an acl in
/etc/squid3/squid.conf for your local network, something like the
following:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    acl localnet src
    192.168.0.0[/]{style="color: #000000; font-weight: bold;"}[16]{style="color: #000000;"}
    [\# RFC1918 possible internal
    network]{style="color: #666666; font-style: italic;"}
    :::
:::
:::

(make sure to change the subnet to match your network) Next, add a rule
allowing access from the local network you just defined:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    http\_access allow localnet
    :::
:::
:::

(If your squid server is on the same box as your drush installation, you
just need to allow localhost)

Restart squid, and away you go.

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [/]{style="color: #000000; font-weight: bold;"}etc[/]{style="color: #000000; font-weight: bold;"}init.d[/]{style="color: #000000; font-weight: bold;"}squid3
    restart
    :::
:::
:::

Using drush with squid
----------------------

To make drush use squid, simply do the following:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [http\_proxy]{style="color: #007800;"}=[\"\<a
    href=\"]{style="color: #ff0000;"}http:[//]{style="color: #000000; font-weight: bold;"}squid-host.example.com:[3128]{style="color: #000000;"}[/]{style="color: #000000; font-weight: bold;"}[\"\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}http:[//]{style="color: #000000; font-weight: bold;"}squid-host.example.com:[3128]{style="color: #000000;"}[/]{style="color: #000000; font-weight: bold;"}[\"\</a\>
    php /usr/local/drush/drush.php dl cck]{style="color: #ff0000;"}
    :::
:::
:::

(You\'ll probably want to add an alias)

Is it working?
--------------

Let\'s try and download the
[inlinetags](http://drupal.org/project/inlinetags) module.\

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    drush-host [\# http\_proxy=\"\<a
    href=\"http://squid-host.example.com:3128/\"\"\>http://squid-host.example.com:3128/\"\</a\>
    php /usr/local/drush/drush.php dl
    inlinetags]{style="color: #666666; font-style: italic;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    squid-host [\# tail -f
    /var/log/squid3]{style="color: #666666; font-style: italic;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [1267120330.674]{style="color: #000000;"}  
     [273]{style="color: #000000;"} 192.168.208.29
    TCP\_MISS[/]{style="color: #000000; font-weight: bold;"}[200]{style="color: #000000;"}
    [8952]{style="color: #000000;"} GET
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}http:[//]{style="color: #000000; font-weight: bold;"}ftp.drupal.org[/]{style="color: #000000; font-weight: bold;"}files[/]{style="color: #000000; font-weight: bold;"}projects[/]{style="color: #000000; font-weight: bold;"}inlinetags-[6]{style="color: #000000;"}.x-[1.1]{style="color: #000000;"}.tar.gz[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"} -
    DIRECT[/]{style="color: #000000; font-weight: bold;"}140.211.166.142
    application[/]{style="color: #000000; font-weight: bold;"}x-gzip
    :::
:::
:::

So, we can tell from the log that the request came into squid, but did
not find the object cached. So far so good. Let\'s try again:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    drush-host [\# http\_proxy=\"\<a
    href=\"http://squid-host.example.com:3128/\"\"\>http://squid-host.example.com:3128/\"\</a\>
    php /usr/local/drush/drush.php dl
    inlinetags]{style="color: #666666; font-style: italic;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    squid-host [\# tail -f
    /var/log/squid3]{style="color: #666666; font-style: italic;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [1267121152.216]{style="color: #000000;"}    
     [0]{style="color: #000000;"} 192.168.208.29
    TCP\_HIT[/]{style="color: #000000; font-weight: bold;"}[200]{style="color: #000000;"}
    [8960]{style="color: #000000;"} GET
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}http:[//]{style="color: #000000; font-weight: bold;"}ftp.drupal.org[/]{style="color: #000000; font-weight: bold;"}files[/]{style="color: #000000; font-weight: bold;"}projects[/]{style="color: #000000; font-weight: bold;"}inlinetags-[6]{style="color: #000000;"}.x-[1.1]{style="color: #000000;"}.tar.gz[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"} -
    NONE[/]{style="color: #000000; font-weight: bold;"}-
    application[/]{style="color: #000000; font-weight: bold;"}x-gzip
    :::
:::
:::

Good news! This time the request never went out to drupal.org. That\'s
all I have for now, hope it helps someone. Please feel free to comment
if you have difficulties with these instructions. (or success!)
:::
:::
:::

