---
layout: post
title: "unusual file system usage in linux"
date: 2014-03-01
---

If you ever come across a situation where the df command and du commands reporting different size of the same file system. The main cause of this are the files being written by applications after the files have been deleted by users on the file system. du/ls command will not show these files. Hence the conflict between du and df. You can view those files using lsof &#124; grep deleted command. Then you can kill those processes or restart the concerned application to reclaim space.

<h3>&#35;df -h</h3>
Filesystem Size Used Avail Use% Mounted on <br>
/dev/mapper/rootvg-rootlv 50G 16G 32G 34% / <br>
tmpfs 3.9G 0 3.9G 0% /dev/shm<br>
/dev/sda1 504M 121M 358M 26% /boot<br>
/dev/sda2 104G 96G 2.8G 98% /local<br>

<h3>&#35;du -sh /local</h3>
11G /local

<h3>&#35;lsof |grep deleted</h3>
httpd 477 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 865 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 1312 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 1393 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 1532 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 2022 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 2640 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 2763 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 2909 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 3047 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
httpd 3048 root 5w REG 253,2 90780834079 9848484 /local/access.log (deleted) <br>
