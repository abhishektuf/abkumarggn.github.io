---
layout: post
title: "monitoring linux host with sar utility"
date: 2019-06-25
---

<h3>you can use sar to monitor your Linux system effectively.

use the below command to redirect output to a file. i.e. to save data for that email to customer :)</h3>
{% highlight language %}
[root@localhost ~]# sar 2 4 -o /tmp/sardata > /dev/null 2>&1
root@abhishek-jumpbox:~# sar 1 1 -o /tmp/sardata > /dev/null 2>&1
{% endhighlight %}

<h3>use the below one to read that file too.</h3>
{% highlight language %}
root@abhishek-jumpbox:~# sar -f /tmp/sardata
Linux 4.15.0-43-generic (abhishek-jumpbox)      06/25/2019      _x86_64_        (8 CPU)

10:49:37 AM     CPU     %user     %nice   %system   %iowait    %steal     %idle
10:49:38 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
10:49:50 AM     all      0.12      0.00      0.05      0.45      0.00     99.38
10:49:51 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
10:50:39 AM     all      0.01      0.00      0.01      0.00      0.00     99.98
10:50:40 AM     all      0.00      0.00      0.00      0.00      0.00    100.00
Average:        all      0.03      0.00      0.02      0.09      0.00     99.86
root@abhishek-jumpbox:~#

{% endhighlight %}

<h3>memory stats using sar</h3>

{% highlight language %}
root@abhishek-jumpbox:~# sar -r 1 1
Linux 4.15.0-43-generic (abhishek-jumpbox)      06/25/2019      _x86_64_        (8 CPU)

10:52:07 AM kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
10:52:08 AM  31672024  32185736   1267344      3.85    182316    641832    827932      2.37    720796    244316         0
Average:     31672024  32185736   1267344      3.85    182316    641832    827932      2.37    720796    244316         0
{% endhighlight %}

<h3>disk stats using sar</h3>
{% highlight language %}
[root@oxygen ~]# sar -d -p 1 1
root@abhishek-jumpbox:~# sar -d -p 1 1
Linux 4.15.0-43-generic (abhishek-jumpbox)      06/25/2019      _x86_64_        (8 CPU)

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