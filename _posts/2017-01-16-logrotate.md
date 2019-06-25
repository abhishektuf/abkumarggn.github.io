---
layout: post
title: "logrotate config for syslogs"
date: 2017-01-16
---

here is an example of logrotate script/config file I use for syslogs.
{% highlight language %}
[root@oxygen ~]# cat /etc/logrotate.d/syslog
/var/log/messages /var/log/secure /var/log/maillog /var/log/spooler /var/log/boot.log /var/log/cron 
{
    rotate 5
    compress
    size 50M
    create 0600 root root
    sharedscripts
    postrotate
        /bin/kill -HUP `cat /var/run/syslogd.pid 2> /dev/null` 2> /dev/null || true
        /bin/kill -HUP `cat /var/run/rsyslogd.pid 2> /dev/null` 2> /dev/null || true
    endscript
}
{% endhighlight %}
