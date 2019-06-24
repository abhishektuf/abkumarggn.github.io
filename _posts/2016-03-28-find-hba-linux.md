---
layout: post
title: "how to find wwn information of hba cards under linux"
date: 2016-03-28
---

On Red Hat Enterprise Linux & openSUSE, you can run below command to get World Wide Name of a HBA card.

# systool -c fc_host -v | grep "port_name"

you can install this tool by

on CentOS/RHEL

#yum install sysfsutils

on Ubuntu/Debian

#apt install sysfsutils

Note : systool command is provided by sysfsutils package.

alternative command for the same thing that should work in any standard Linux kernel.

# cat /sys/class/scsi_host/host*/device/fc_host/host*/node_name
