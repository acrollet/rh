---
layout: post
title: "Setting up nagios3 to send prowl notifications"
date: 2009-07-14 22:12:49 +0000
categories: ["perl", "bash", "debian", "prowl", "nagios"]
permalink: /content/setting-nagios3-send-prowl-notifications
---



*Updated 27.i.2010 to reflect mig5\'s corrections*

I spent a few minutes today setting up our nagios install at work to
page me via [prowl](http://prowl.weks.net/), instead of an email-\>sms
gateway. Why? Because I\'m cheap, that\'s why - don\'t like paying for
any more texts than I must. I ran into a few gotchas, so I thought I
would briefly document the process.

First, you must download the perl script that will send prowl
notifications.\


``` sh
sudo mkdir -p /usr/local/bin
sudo wget -O /usr/local/bin/prowl.pl <a href="http://prowl.weks.net/static/prowl.pl
sudo">http://prowl.weks.net/static/prowl.pl
sudo</a> chmod +x /usr/local/bin/prowl.pl
```

Next, you will have to install the Crypt::SSLeay and LWP::UserAgent
library for perl, so it can access https URLs.\


``` sh
# If you're running debian/ubuntu
sudo apt-get update; sudo apt-get install libcrypt-ssleay-perl liblwp-useragent-determined-perl
# otherwise find a package for your distro, or run:
# sudo cpan install Crypt::SSLeay
# sudo cpan install LWP::UserAgent
```


Now, try it out to be sure it works:


``` sh
/usr/local/bin/prowl.pl -apikey='yourAPIkeyHere' -application='prowl.pl' -event='test' -notification='mic check 1 2'
```


You should get a \'Notification successfully posted.\' message. (and a
popup on your phone, of course!) If the script isn\'t working, you\'ll
have to figure out the reason, because nagios depends on it.

Once you\'ve ironed all that out, it\'s time to configure nagios!

First, you need to set up your contact information. Edit whichever file
you keep your contacts in, and modify an existing record, or add a new
one, similar to this:


``` perl
define contact{
    contact_name                    adrian_pager
    alias                           Adrian Rollett
    service_notification_period     24x7
    host_notification_period        24x7
    service_notification_options    w,u,c,r
    host_notification_options       d,u,r
    service_notification_commands   notify-service-by-prowl
    host_notification_commands      notify-host-by-prowl
    _prowl_apikey                   yourAPIkeyGoesHere
    }
```

It is very important that you leave the underscore in front of the
\_prowl\_apikey variable, as Nagios\' custom variables [depend on
it](http://nagios.sourceforge.net/docs/3_0/customobjectvars.html).

Next, you\'ll need to add the custom prowl notification commands. Edit
the appropriate file, and add these commands:


``` perl
define command{
        command_name notify-host-by-prowl
        command_line /usr/bin/perl -w /usr/local/bin/prowl.pl -apikey="$_CONTACTPROWL_APIKEY$" -priority=1 -application="Nagios" -event="Host" -notification="$HOSTNAME$ $HOSTDESC$ '$HOSTOUTPUT$'"
}
 
define command{
        command_name notify-service-by-prowl
        command_line /usr/bin/perl -w /usr/local/bin/prowl.pl -apikey="$_CONTACTPROWL_APIKEY$" -priority=1 -application="Nagios" -event="Service" -notification="$HOSTNAME$ $SERVICEDESC$ '$SERVICEOUTPUT$'"
}
```


If your perl binary doesn\'t live in /usr/bin, be sure to give the
correct path. (run \'which perl\' to find this out if you don\'t know)
If you try to run the prowl.pl script directly, (without using the
system perl binary) nagios uses its own perl interpreter, and you\'ll
get an error similar to this in the nagios logs:


``` sh
*ePN failed to compile /usr/local/bin/prowl.pl: "Missing right curly or square bracket at (eval 1) line 95, at end of line syntax error at (eval 1) line 102, at EOF"
```


If you have any trouble, check the nagios debug logs, (you may need to
turn up the nagios debug level) and try to run the command it\'s
producing as the nagios user.




