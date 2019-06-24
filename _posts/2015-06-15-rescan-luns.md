---
layout: post
title: "rescan new lun/ vdisk in linux"
date: 2015-06-15
---

Use below for loop to detect new LUN assignments on existing HBA

#for host in `ls /sys/class/scsi_host/`;
do echo "- - -" >/sys/class/scsi_host/${host}/scan
done

echo "c t l" >  /sys/class/scsi_host/hostH/scan

Now rescan each of these devices.

The three values stand for channel, target, and LUN. The dashes act as wildcards meaning "rescan everything"

Use below commands when you are expanding existing disk in VM.

[root@rhel7test1 ~]# ls /sys/class/scsi_device/
2:0:0:0  2:0:1:0  2:0:2:0  2:0:3:0  3:0:0:0

[root@rhel7test1 ~]# echo 1> /sys/class/scsi_device/2\:0\:0\:0/device/rescan
[root@rhel7test1 ~]# echo 1> /sys/class/scsi_device/2\:0\:1\:0/device/rescan
[root@rhel7test1 ~]# echo 1> /sys/class/scsi_device/2\:0\:2\:0/device/rescan
[root@rhel7test1 ~]# echo 1> /sys/class/scsi_device/2\:0\:3\:0/device/rescan
[root@rhel7test1 ~]# echo 1> /sys/class/scsi_device/3\:0\:0\:0/device/rescan

You can also use rescan-scsi-bus.sh utility. Install the sg3_utils package

[root@rhel7test1 ~]# rescan-scsi-bus.sh
which: no multipath in (/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin)
Scanning SCSI subsystem for new devices
Scanning host 0 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 1 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 2 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
 Scanning for device 2 0 0 0 ...
OLD: Host: scsi2 Channel: 00 Id: 00 Lun: 00
      Vendor: VMware   Model: Virtual disk     Rev: 1.0
      Type:   Direct-Access                    ANSI SCSI revision: 02
 Scanning for device 2 0 1 0 ...
OLD: Host: scsi2 Channel: 00 Id: 01 Lun: 00
      Vendor: VMware   Model: Virtual disk     Rev: 1.0
      Type:   Direct-Access                    ANSI SCSI revision: 02
 Scanning for device 2 0 2 0 ...
OLD: Host: scsi2 Channel: 00 Id: 02 Lun: 00
      Vendor: VMware   Model: Virtual disk     Rev: 1.0
      Type:   Direct-Access                    ANSI SCSI revision: 02
 Scanning for device 2 0 3 0 ...
OLD: Host: scsi2 Channel: 00 Id: 03 Lun: 00
      Vendor: VMware   Model: Virtual disk     Rev: 1.0
      Type:   Direct-Access                    ANSI SCSI revision: 02
Scanning host 3 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
 Scanning for device 3 0 0 0 ...
OLD: Host: scsi3 Channel: 00 Id: 00 Lun: 00
      Vendor: NECVMWar Model: VMware SATA CD00 Rev: 1.00
      Type:   CD-ROM                           ANSI SCSI revision: 05
Scanning host 4 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 5 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 6 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 7 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 8 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 9 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 10 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 11 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 12 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 13 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 14 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 15 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 16 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 17 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 18 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 19 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 20 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 21 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 22 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 23 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 24 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 25 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 26 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 27 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 28 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 29 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 30 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 31 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
Scanning host 32 for  SCSI target IDs  0 1 2 3 4 5 6 7, all LUNs
0 new or changed device(s) found.
0 remapped or resized device(s) found.
0 device(s) removed.
