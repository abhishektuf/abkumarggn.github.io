---
layout: post
title: "get list of memory consuming processes"
date: 2017-02-17
---

the below two commands will provide you the processes which are consuming maximum memory on Linux machine.
{% highlight language %}
#ps -A --sort -rss -o comm,pmem | head -10
#ps axu | awk '{print $2, $3, $4, $11}' | head -1 && ps axu | awk '{print $2, $3, $4, $11}' | sort -k3 -nr |head -10
{% endhighlight %}
