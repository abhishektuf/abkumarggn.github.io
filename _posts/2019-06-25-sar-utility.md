---
layout: post
title: "monitoring linux host with sar utility"
date: 2019-06-25
---
This post is related to sysstat(System Activity Reporter) utilty to view/generate historical performance data of a Linux server.

Installation is simple using your distribution's package manager 

for CentOS/RHEL based servers
{% highlight language %}
sudo yum install sysstat
{% endhighlight %}
for Ubuntu/Debian based servers
{% highlight language %}
sudo apt install sysstat
{% endhighlight %}

now enable the data capture by modifying the file per below.
{% highlight language %}
root@localhost:~# cat /etc/default/sysstat
#
# Default settings for /etc/init.d/sysstat, /etc/cron.d/sysstat
# and /etc/cron.daily/sysstat files
#

# Should sadc collect system activity informations? Valid values
# are "true" and "false". Please do not put other values, they
# will be overwritten by debconf!
ENABLED="true"
{% endhighlight %}
now enable & start the sysstat service in systemd.
{% highlight language %}
sudo systemctl enable sysstat
Synchronizing state of sysstat.service with SysV service script with /lib/systemd/systemd-sysv-install.
sudo systemctl start sysstat
{% endhighlight %}
<h3>use the below command to redirect output to a file. i.e. to save data for that email to customer :)</h3>
{% highlight language %}
[root@localhost ~]# sar 2 4 -o /tmp/sardata > /dev/null 2>&1
{% endhighlight %}

<h3>use the below one to read that file too.</h3>
{% highlight language %}
root@localhost:~# sar -f /tmp/sardata
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

10:49:37 AM     CPU     %user     %nice   %system   %iowait    %steal     %idle
10:49:38 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
10:49:50 AM     all      0.12      0.00      0.05      0.45      0.00     99.38
10:49:51 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
10:50:39 AM     all      0.01      0.00      0.01      0.00      0.00     99.98
10:50:40 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
Average:        all      0.03      0.00      0.02      0.09      0.00     99.86
root@localhost:~#

{% endhighlight %}

<h3>cpu stats using sar</h3>
{% highlight language %}
root@localhost:~# sar -u 2 5
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

11:46:18 AM     CPU     %user     %nice   %system   %iowait    %steal     %idle
11:46:20 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
11:46:22 AM     all      0.00      0.00      0.06      0.00      0.00     99.94
11:46:24 AM     all      0.06      0.00      0.00      0.00      0.00     99.94
11:46:26 AM     all      0.00      0.00      0.06      0.00      0.00     99.94
11:46:28 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
Average:        all      0.01      0.00      0.03      0.00      0.00     99.96
root@localhost:~#
{% endhighlight %}

<h3>memory stats using sar</h3>

{% highlight language %}
root@localhost:~# sar -r 1 1
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

10:52:07 AM kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
10:52:08 AM  31672024  32185736   1267344      3.85    182316    641832    827932      2.37    720796    244316         0
Average:     31672024  32185736   1267344      3.85    182316    641832    827932      2.37    720796    244316         0
{% endhighlight %}

<h3>disk stats using sar</h3>
{% highlight language %}
[root@oxygen ~]# sar -d -p 1 1
root@localhost:~# sar -d -p 1 1
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

10:52:29 AM       DEV       tps     rkB/s     wkB/s   areq-sz    aqu-sz     await     svctm     %util
10:52:30 AM     loop0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
10:52:30 AM     loop1      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
10:52:30 AM     loop2      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
10:52:30 AM       vda      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

Average:          DEV       tps     rkB/s     wkB/s   areq-sz    aqu-sz     await     svctm     %util
Average:        loop0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:        loop1      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:        loop2      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:          vda      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

{% endhighlight %}

<h3>check run queue length</h3>
{% highlight language %}
root@localhost:~# sar -q 2 2
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

11:48:06 AM   runq-sz  plist-sz   ldavg-1   ldavg-5  ldavg-15   blocked
11:48:08 AM         0       214      0.00      0.00      0.00         0
11:48:10 AM         0       215      0.00      0.00      0.00         0
Average:            0       214      0.00      0.00      0.00         0
root@localhost:~#
{% endhighlight %}

<h3>check network stats</h3>
{% highlight language %}
root@localhost:~# sar -n DEV 1 1
Linux 4.15.0-43-generic (localhost)      06/25/2019      _x86_64_        (8 CPU)

11:48:56 AM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
11:48:57 AM   docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
11:48:57 AM      eth0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
11:48:57 AM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

Average:        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
Average:      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:         eth0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
root@localhost:~#
{% endhighlight %}
