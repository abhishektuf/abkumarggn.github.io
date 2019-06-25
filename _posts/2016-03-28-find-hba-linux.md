---
layout: post
title: "how to find wwn information of hba cards under linux"
date: 2016-03-28
---

On Red Hat Enterprise Linux & openSUSE, you can run below command to get World Wide Name of a HBA card.

<h3>&#35;systool -c fc_host -v | grep "port_name"</h3>

you can install this tool by

on CentOS/RHEL

<h3>&#35;yum install sysfsutils</h3>

on Ubuntu/Debian

<h3>&#35;apt install sysfsutils</h3>

Note : systool command is provided by sysfsutils package.

alternative command for the same thing that should work in any standard Linux kernel.

<h3>&#35;cat /sys/class/scsi_host/host*/device/fc_host/host*/node_name</h3>
