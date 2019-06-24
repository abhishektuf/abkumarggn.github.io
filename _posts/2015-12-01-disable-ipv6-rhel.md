---
layout: post
title: "disable ipv6 on rhel/centos version 5 / 6 / 7"
date: 2015-12-01
---

{% highlight language %}
on RHEL5

# cat /proc/sys/net/ipv6/conf/all/disable_ipv6
0
# echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6
# cat /proc/sys/net/ipv6/conf/all/disable_ipv6
1


on RHEL6 and RHEL7

# cat /proc/sys/net/ipv6/conf/all/disable_ipv6
0
# cat /proc/sys/net/ipv6/conf/default/disable_ipv6
0
# echo 1 > /proc/sys/net/ipv6/conf/default/disable_ipv6
# echo 1 > /proc/sys/net/ipv6/conf/all/disable_ipv6
# cat /proc/sys/net/ipv6/conf/all/disable_ipv6
1
# cat /proc/sys/net/ipv6/conf/default/disable_ipv6
1
{% endhighlight %}
