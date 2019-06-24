---
layout: post
title: "recover system after /boot partition is deleted on linux"
date: 2014-01-13
---

recover your system in the event of /boot partition lost/ deletion/ or accidental rm of all files under /boot

if you face such scenario at your any centos / rhel /fedora systems. don't panic you can still recover your system , just follow the below steps -



1. boot your system using rescue mode available on centos dvd or cd ISO
2. now chroot to the mounted the filesystem
3. go to the cdrom mount under /media and go to where rpm's are stored (/media/cdrom/Packages) 
4. install kernel, grub and redhat-logs rpms using --force parameter
5. generate initrd using mkinitrd command 6. create a new /boot/grub/grub.conf file per example below

default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm.gz
hiddenmenu
title CentOS
root (hd0,0)
kernel /vmlinuz-2.6.279-164.el6 ro root=
initrd /initrd-2.6.279-164.el6.img@@

7. make a softlink
#ln -s /boot/grub/grub.conf /boot/grub/menu.lst

Note : make sure you have correct UUID or parition label
