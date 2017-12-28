---
layout: post
title: "Setting up nagios3 to send prowl notifications"
date: 2009-07-14 22:12:49 +0000
categories: ["perl", "bash", "debian", "prowl", "nagios"]
permalink: /content/setting-nagios3-send-prowl-notifications
---
::: {.field .field-name-body .field-type-text-with-summary .field-label-hidden}
::: {.field-items}
::: {.field-item .even}
*Updated 27.i.2010 to reflect mig5\'s corrections*

I spent a few minutes today setting up our nagios install at work to
page me via [prowl](http://prowl.weks.net/), instead of an email-\>sms
gateway. Why? Because I\'m cheap, that\'s why - don\'t like paying for
any more texts than I must. I ran into a few gotchas, so I thought I
would briefly document the process.

First, you must download the perl script that will send prowl
notifications.\

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [sudo]{style="color: #c20cb9; font-weight: bold;"}
    [mkdir]{style="color: #c20cb9; font-weight: bold;"}
    [-p]{style="color: #660033;"}
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [sudo]{style="color: #c20cb9; font-weight: bold;"}
    [wget]{style="color: #c20cb9; font-weight: bold;"}
    [-O]{style="color: #660033;"}
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    [\<]{style="color: #000000; font-weight: bold;"}a
    [href]{style="color: #007800;"}=[\"http://prowl.weks.net/static/prowl.pl]{style="color: #ff0000;"}
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [sudo\"]{style="color: #ff0000;"}[\>]{style="color: #000000; font-weight: bold;"}http:[//]{style="color: #000000; font-weight: bold;"}prowl.weks.net[/]{style="color: #000000; font-weight: bold;"}static[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [sudo]{style="color: #c20cb9; font-weight: bold;"}[\</]{style="color: #000000; font-weight: bold;"}a[\>]{style="color: #000000; font-weight: bold;"}
    [chmod]{style="color: #c20cb9; font-weight: bold;"} +x
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    :::
:::
:::

Next, you will have to install the Crypt::SSLeay and LWP::UserAgent
library for perl, so it can access https URLs.\

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# If you\'re running
    debian/ubuntu]{style="color: #666666; font-style: italic;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [sudo]{style="color: #c20cb9; font-weight: bold;"} [apt-get
    update]{style="color: #c20cb9; font-weight: bold;"};
    [sudo]{style="color: #c20cb9; font-weight: bold;"} [apt-get
    install]{style="color: #c20cb9; font-weight: bold;"}
    libcrypt-ssleay-perl liblwp-useragent-determined-perl
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# otherwise find a package for your distro, or
    run:]{style="color: #666666; font-style: italic;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# sudo cpan install
    Crypt::SSLeay]{style="color: #666666; font-style: italic;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\# sudo cpan install
    LWP::UserAgent]{style="color: #666666; font-style: italic;"}
    :::
:::
:::

Now, try it out to be sure it works:\

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    [-apikey]{style="color: #660033;"}=[\'yourAPIkeyHere\']{style="color: #ff0000;"}
    [-application]{style="color: #660033;"}=[\'prowl.pl\']{style="color: #ff0000;"}
    [-event]{style="color: #660033;"}=[\'test\']{style="color: #ff0000;"}
    [-notification]{style="color: #660033;"}=[\'mic check 1
    2\']{style="color: #ff0000;"}
    :::
:::
:::

You should get a \'Notification successfully posted.\' message. (and a
popup on your phone, of course!) If the script isn\'t working, you\'ll
have to figure out the reason, because nagios depends on it.

Once you\'ve ironed all that out, it\'s time to configure nagios!

First, you need to set up your contact information. Edit whichever file
you keep your contacts in, and modify an existing record, or add a new
one, similar to this:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    define contact[{]{style="color: #7a0874; font-weight: bold;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        contact\_name                    adrian\_pager
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        [alias]{style="color: #7a0874; font-weight: bold;"}            
                  Adrian Rollett
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        service\_notification\_period     24x7
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        host\_notification\_period        24x7
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        service\_notification\_options  
     [w]{style="color: #c20cb9; font-weight: bold;"},u,c,r
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        host\_notification\_options       d,u,r
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        service\_notification\_commands   notify-service-by-prowl
    :::

9.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        host\_notification\_commands      notify-host-by-prowl
    :::

10. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        \_prowl\_apikey                   yourAPIkeyGoesHere
    :::

11. ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
        [}]{style="color: #7a0874; font-weight: bold;"}
    :::
:::
:::

It is very important that you leave the underscore in front of the
\_prowl\_apikey variable, as Nagios\' custom variables [depend on
it](http://nagios.sourceforge.net/docs/3_0/customobjectvars.html).

Next, you\'ll need to add the custom prowl notification commands. Edit
the appropriate file, and add these commands:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    define
    [command]{style="color: #7a0874; font-weight: bold;"}[{]{style="color: #7a0874; font-weight: bold;"}
    :::

2.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            command\_name notify-host-by-prowl
    :::

3.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            command\_line
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}[perl]{style="color: #c20cb9; font-weight: bold;"}
    [-w]{style="color: #660033;"}
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    [-apikey]{style="color: #660033;"}=[\"[\$\_CONTACTPROWL\_APIKEY]{style="color: #007800;"}\$\"]{style="color: #ff0000;"}
    [-priority]{style="color: #660033;"}=[1]{style="color: #000000;"}
    [-application]{style="color: #660033;"}=[\"Nagios\"]{style="color: #ff0000;"}
    [-event]{style="color: #660033;"}=[\"Host\"]{style="color: #ff0000;"}
    [-notification]{style="color: #660033;"}=[\"[\$HOSTNAME]{style="color: #007800;"}\$
    [\$HOSTDESC]{style="color: #007800;"}\$
    \'[\$HOSTOUTPUT]{style="color: #007800;"}\$\'\"]{style="color: #ff0000;"}
    :::

4.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::

5.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
     
    :::

6.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    define
    [command]{style="color: #7a0874; font-weight: bold;"}[{]{style="color: #7a0874; font-weight: bold;"}
    :::

7.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            command\_name notify-service-by-prowl
    :::

8.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
            command\_line
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}[perl]{style="color: #c20cb9; font-weight: bold;"}
    [-w]{style="color: #660033;"}
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl
    [-apikey]{style="color: #660033;"}=[\"[\$\_CONTACTPROWL\_APIKEY]{style="color: #007800;"}\$\"]{style="color: #ff0000;"}
    [-priority]{style="color: #660033;"}=[1]{style="color: #000000;"}
    [-application]{style="color: #660033;"}=[\"Nagios\"]{style="color: #ff0000;"}
    [-event]{style="color: #660033;"}=[\"Service\"]{style="color: #ff0000;"}
    [-notification]{style="color: #660033;"}=[\"[\$HOSTNAME]{style="color: #007800;"}\$
    [\$SERVICEDESC]{style="color: #007800;"}\$
    \'[\$SERVICEOUTPUT]{style="color: #007800;"}\$\'\"]{style="color: #ff0000;"}
    :::

9.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [}]{style="color: #7a0874; font-weight: bold;"}
    :::
:::
:::

If your perl binary doesn\'t live in /usr/bin, be sure to give the
correct path. (run \'which perl\' to find this out if you don\'t know)
If you try to run the prowl.pl script directly, (without using the
system perl binary) nagios uses its own perl interpreter, and you\'ll
get an error similar to this in the nagios logs:

::: {.geshifilter}
::: {.bash .geshifilter-bash style="font-family:monospace;"}
1.  ::: {style="font-family: monospace; font-weight: normal; font-style: normal"}
    [\*]{style="color: #000000; font-weight: bold;"}ePN failed to
    compile
    [/]{style="color: #000000; font-weight: bold;"}usr[/]{style="color: #000000; font-weight: bold;"}local[/]{style="color: #000000; font-weight: bold;"}bin[/]{style="color: #000000; font-weight: bold;"}prowl.pl:
    [\"Missing right curly or square bracket at (eval 1) line 95, at end
    of line syntax error at (eval 1) line 102, at
    EOF\"]{style="color: #ff0000;"}
    :::
:::
:::

If you have any trouble, check the nagios debug logs, (you may need to
turn up the nagios debug level) and try to run the command it\'s
producing as the nagios user.
:::
:::
:::

