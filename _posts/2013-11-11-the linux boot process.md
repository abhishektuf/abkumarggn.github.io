---
layout: post
title: "the linux boot process"
date: 2013-11-11
---

Friends last few days were so busy days for most of my seniors. Actually one of our client had accidentally deleted some important configuration files from server. We did lot’s of troubleshooting to bring daemons and server up. Just wanted to share my thoughts for your knowledge. For me it was like practical review of Linux kernel boot sequence.

Let me share some boot process parts.



A) BIOS initialization

BIOS is the interface between hardware & software in very basic level. It runs POST, and then it looks for peripherals & a device to boot from. at the end of POST , a boot device is selected from list of detected boot device.(it may be floopy,hddcd-rom,NIC)

B) Boot loader

BIOS reads & executes the 1st physical sector of chosen boot media on system. Usually this is contained in the 1st 446 byte of hard disk (in case of GRUB)

B.1. So BIOS 1st pass control to IPL within MBR.(This stage is called 1st stage of booting of Linux)

Note: – If there are multiple OS are installed then boot loader must be configured to pass control to other desired OS.

B.2. If 1st stage of booting pass control to Linux then it seeks /boot partition & by finding grob.conf,initrd & other files it completed 2nd stage of booting.

C) Kernel initialization: – lots of process generated for compiling device driver & to attempt to locate their corresponding drivers.

You can see /var/log/dmesg that contains snapshot of kernel messages taken just after control pass to init.

Note: – if essential (needed for boot) drivers have been compiled as modules instead of into the kernel, and then they must be include in initrd.img. This is then temporarily mounted by kernel on RAM disk to make modules available for initialization process.

After loading of all essential drivers, kernel mounts root file system (/) read-only & pass the control to 1st process (init).

D) INIT:- init reads /etc/inittab (because now / is read-only) & execute all that written in this file as follows

1) Selection of desired run level

2) Execute /etc/rc.d/rc.sysinit

A) Activate udev & selinux

B) Set kernel parameter from /etc/sysctl.conf

C) Set system clock

D) Enable swap partition

E) Set hostname

F) Checking root file system & remount (in read write mode)

G) Activate RAID & LVM

H) Enable disk Quota

I) Check & mount other file system read write mode

J) Clean up stale lock & PID files

3) Runs /etc/rc.d/rc?.d/

(/etc/rc.d/init.d has soft links for corresponding run levels)

4) It runs /etc/rc.d/rc.local

5) It starts xinetd service.

This completes the boot process for the Linux kernel.



LINUX BOOTING SEQUENCE TROUBLESHOOTING

Case 1: No boot loader splash screen or prompt appears

Cause:

1) Grub.conf miss configures

2) Initrd misplaced or deleted

3) MBR cruuppet

4) /boot partition miss

Grub.conf miss configures

Remedy: try to pass boot location initrd location & kernel module location as follows

Step a)

Grub > root (hd0,0)

Note: here hd0,0 means boot partition is in 1st partition of 1st hdd.(please use hd for SATA & SCSI hdd also )

Step b)

grub > kernel /vmlinuz-$(uname -r) root=LABEL=/ rhgb quiet

Step c)

grub > initrd /initrd-$(uname -r).img

Step d)

grub > boot

Then after rebooting try to recreate grub.conf file

Initrd misplaced or deleted

Case a) system is up

This is the most fortunate situation for system admins who are managing the server remotely because now once the system will down it will not be up without rescue mode

Remedy:

root@dh-localhost ~# mkinitrd /boot/ initrd-$(uname -r).img $(uname -r)

Case b) system is down

Then boot from system via DVD & start it by rescue mode

Remedy:

Step 1)

Boot: linux recue

After some process & ittrective prompt you will be on sh prompt

Step 2)

chroot /mnt/sysimage

cd /boot

mkinitrd /boot/ initrd-$(uname -r).img $(uname -r)

Then reboot the system by HDD

Note: – in case of fstab is also misconfigured (ie / & other partition will not mount after boot) then chroot command will not work. So in this case your 1st step would be to correct fstab then perform above steps as follows

Step a) boot from DVD or other bootable media

Step b) chroot /mnt/sysimage (you will find chroot error here )

Step c) mkdir /test

e2label /dev/sda1 (if it will show boot them mount it otherwise try to search by e2label/dev/sda2 ownwards)

mount /dev/sda1 /test

cd /test

cd grub

vi grub.conf (please make it correct)

mkdir /data

mount /dev/sda2 /data (mounting / partition on /data )

cd /data

cd /etc

vi fstab (please correct it )

Then reboot the system & follow previous step

Mbr corrupt

Case a) system is up

Method 1

root@localhost ~# /sbin/grub-install /dev/sda

Method 2

root@localhost ~# grub

grub> root (hd0,0)

grub > setup (hd0)

grub > quit

Case b) system is down

Boot system by rescue mode

Sh # chroot /mnt/sysimage

Sh # /sbin/grub-install /dev/sda

Note : A smart system admin always take backup of MBR as follows

root@localhost ~# dd if=/home/mbr of=/home/mbr bs=1 count 500

&

For restoration for MBR

root@localhost ~# dd if=/home/mbr of=/home/mbr bs=1 count 500


/boot partition missing

In this case if you have backup of /boot then you can recover it otherwise you need to rebuild the server again.

Today while reading online forums related to boot process I came across a very good article which explained not only what is boot process for linux but also what are the components of this process. the article can be read at the links at end of this article. Not only this someone at the same page referred bootchart utility to map out the complete boot process with measurements. I tried and install bootchart from fedora default repositories and its awesome , this is the image it produced.




References ---
http://www.ibm.com/developerworks/library/l-linuxboot/
http://unix.stackexchange.com/questions/27034/please-explain-linux-boot-sequence-in-detail
http://0pointer.de/blog/projects/systemd.html
http://www.youtube.com/watch?v=TyMLi8QF6sw
