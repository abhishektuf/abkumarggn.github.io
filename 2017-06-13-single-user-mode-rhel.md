---
layout: post
title: "boot RHEL7/Centos 7 in single user mode"
date: 2017-06-13
---

if you want to boot into single user mode of RHEL7 or Centos 7 in order to reset root password or do any other recovery work. You can follow the steps below.

1. Boot or reboot the server
2. Go to Grub2 OS boot selection menu
3. press e to go into edit mode.
4. append init=/bin/sh to line starting with linux.
5. Press Ctrl+x to boot to shell prompt
6. Now you can remount root partition with rw option ( #mount -o remount,rw /)
7. then change the password using passwd command.
