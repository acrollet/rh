---
layout: post
title: "Using squid as a caching server for drush module downloads"
date: 2010-02-25 18:07:36 +0000
tags: ["drupal", "drush", "proxy"]
permalink: /using-squid-caching-server-drush-module-downloads
---

Intro
-----

Due to [popular request](http://drupal.org/node/698104#comment-2645318),
I've decided to quickly document how we at [UNT Web
support](https://webadmin.unt.edu) use
[squid](http://www.squid-cache.org/) as a proxy caching server for
[drush](http://drupal.org/project/drush). The main goal was to speed up
module updates, and reduce the load on drupal.org and UNT's internet
connection. The instructions are based on my memory, and are for
[Debian](http://debian.org), so there may be gaps here and there
depending on your experience/OS.

Squid Setup
-----------

Installation was super-simple. (gotta love apt)

``` sh
apt-get install squid3
```

Configuration was also quite simple. Basically, the debian package for
squid is setup fairly nicely as a proxy caching server out of the box,
and you need only configure access. First, add an acl in
/etc/squid3/squid.conf for your local network, something like the
following:

``` sh
acl localnet src 192.168.0.0/16 # RFC1918 possible internal network
```

(make sure to change the subnet to match your network) Next, add a rule
allowing access from the local network you just defined:

``` sh
http_access allow localnet
```

(If your squid server is on the same box as your drush installation, you
just need to allow localhost)

Restart squid, and away you go.


``` sh
/etc/init.d/squid3 restart
```


Using drush with squid
----------------------

To make drush use squid, simply do the following:


``` sh
http_proxy="http://squid-host.example.com:3128/" php /usr/local/drush/drush.php dl cck
```

(You'll probably want to add an alias)

Is it working?
--------------

Let's try and download the
[inlinetags](http://drupal.org/project/inlinetags) module.


``` sh
drush-host # http_proxy="<a href="http://squid-host.example.com:3128/"">http://squid-host.example.com:3128/"</a> php /usr/local/drush/drush.php dl inlinetags
squid-host # tail -f /var/log/squid3
1267120330.674    273 192.168.208.29 TCP_MISS/200 8952 GET <a href="http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz">http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz</a> - DIRECT/140.211.166.142 application/x-gzip
```


So, we can tell from the log that the request came into squid, but did
not find the object cached. So far so good. Let's try again:


```
drush-host # http_proxy="<a href="http://squid-host.example.com:3128/"">http://squid-host.example.com:3128/"</a> php /usr/local/drush/drush.php dl inlinetags
squid-host # tail -f /var/log/squid3
1267121152.216      0 192.168.208.29 TCP_HIT/200 8960 GET <a href="http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz">http://ftp.drupal.org/files/projects/inlinetags-6.x-1.1.tar.gz</a> - NONE/- application/x-gzip
```


Good news! This time the request never went out to drupal.org. That's
all I have for now, hope it helps someone. Please feel free to comment
if you have difficulties with these instructions. (or success!)
