---
layout: post
title: "rescan the increased fc lun size in RHEL"
date: 2018-08-04
---

{% highlight language %}

[root@oxygen ~]# multipath -ll mpathb
mpathb (9mxD76oL/xPu9FBVIItP6wFFt9Y23/A7Lw73wOd9bLRb) dm-0 DGC,VRAID
size=200G features='1 queue_if_no_path' hwhandler='1 emc' wp=rw
|-+- policy='round-robin 0' prio=1 status=active
| |- 1:0:1:1  sdk  8:160  active ready running
| `- 2:0:1:1  sdaa 65:160 active ready running
`-+- policy='round-robin 0' prio=0 status=enabled
  |- 1:0:0:1  sdc  8:32   active ready running
  `- 2:0:0:1  sds  65:32  active ready running
[root@oxygen ~]# echo 1 &gt; /sys/block/sdk/device/rescan
[root@oxygen ~]# echo 1 &gt; /sys/block/sdaa/device/rescan
[root@oxygen ~]# echo 1 &gt; /sys/block/sdc/device/rescan
[root@oxygen ~]# echo 1 &gt; /sys/block/sds/device/rescan
[root@oxygen ~]# multipathd -k
multipathd> resize map mpathb
ok
multipathd>
[root@oxygen ~]# multipath -ll mpathb
mpathb (9mxD76oL/xPu9FBVIItP6wFFt9Y23/A7Lw73wOd9bLRb) dm-0 DGC,VRAID
size=700G features='1 queue_if_no_path' hwhandler='1 emc' wp=rw
|-+- policy='round-robin 0' prio=1 status=enabled
| |- 1:0:1:1  sdk  8:160  active ready running
| `- 2:0:1:1  sdaa 65:160 active ready running
`-+- policy='round-robin 0' prio=0 status=enabled
  |- 1:0:0:1  sdc  8:32   active ready running
  `- 2:0:0:1  sds  65:32  active ready running
[root@oxygen ~]# pvs
  PV                   VG       Fmt  Attr PSize   PFree 
  /dev/mapper/mpathb   datavg   lvm2 a--  200.00g      0 
[root@oxygen ~]# pvresize  /dev/mapper/mpathb
  Physical volume "/dev/mapper/mpathb" changed
  1 physical volume(s) resized / 0 physical volume(s) not resized
[root@oxygen ~]# pvs
  PV                   VG       Fmt  Attr PSize   PFree 
  /dev/mapper/mpathb   datavg   lvm2 a--  700.00g 500.00g

{% endhighlight %}
