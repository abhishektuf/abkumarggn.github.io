---
layout: post
title: "monitoring linux host with sar utility"
date: 2015-11-24
---

you can use sar to monitor your Linux system effectively.

use the below command to redirect output to a file. i.e. to save data for that email to customer :)
[root@localhost ~]# sar -f /tmp/sardata


[root@localhost ~]# sar 2 4 -o /tmp/sardata > /dev/null 2>&1

now you can use the below one to read that file too.

[root@oxygen ~]# sar -f /var/log/sa/sa01
Linux 2.6.32-504.8.1.el6.x86_64 (oxygen)   06/01/20XX      _x86_64_        (4 CPU)

12:00:01 AM     CPU     %user     %nice   %system   %iowait    %steal     %idle
12:10:01 AM     all      0.11     10.75      4.47      0.02      0.00     84.66
12:20:01 AM     all      0.08     11.07      4.56      0.01      0.00     84.29
12:30:01 AM     all      0.08     10.68      4.37      0.01      0.00     84.87
12:40:01 AM     all      0.08      9.94      4.07      0.00      0.00     85.90
12:50:01 AM     all      0.08      9.15      3.95      0.01      0.00     86.81
01:00:01 AM     all      0.07      9.75      4.37      0.01      0.00     85.80
01:10:01 AM     all      0.07      9.08      3.85      0.02      0.00     86.98
01:20:01 AM     all      0.07      9.14      3.81      0.01      0.00     86.97
01:30:01 AM     all      0.07      9.58      3.88      0.34      0.00     86.12
01:40:01 AM     all      0.07      9.30      3.80      0.08      0.00     86.75
01:50:01 AM     all      0.07      9.49      3.81      0.03      0.00     86.60

memory stats using sar

[root@oxygen ~]# sar -r 1 1
Linux 2.6.32-504.8.1.el6.x86_64 (oxygen)   06/06/20XX      _x86_64_        (4 CPU)

07:29:28 AM kbmemfree kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit
07:29:29 AM  10752692   5581480     34.17     81152   1423220   1058436      5.16
Average:     10752692   5581480     34.17     81152   1423220   1058436      5.16


disk stats using sar

[root@oxygen ~]# sar -d -p 1 1
Linux 2.6.32-504.8.1.el6.x86_64 (oxygen)   06/06/20XX      _x86_64_        (4 CPU)

07:28:04 AM       DEV       tps  rd_sec/s  wr_sec/s  avgrq-sz  avgqu-sz     await     svctm     %util
07:28:05 AM      scd0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM       sdb      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM       sda      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-root_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-swap_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM datavg-datalv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM infravg-images_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-usr_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-opt_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-tmp_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-var_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-home_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
07:28:05 AM rootvg-system_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

Average:          DEV       tps  rd_sec/s  wr_sec/s  avgrq-sz  avgqu-sz     await     svctm     %util
Average:         scd0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:          sdb      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:          sda      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-root_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-swap_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    datavg-datalv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    infravg-images_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-usr_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-opt_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-tmp_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-var_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-home_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:    rootvg-system_lv      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
