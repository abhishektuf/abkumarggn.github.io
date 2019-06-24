---
layout: post
title: "ftp password change error on parallels plesk"
date: 2012-11-12
---

Another day in system admin lifestyle and I came across an issue on plesk on CentOS version 5

when you try to change the password for any domain’s ftp user , the below error was being displayed on plesk control panel

Error: system user update is failed: Unable to create system user: usermng: PAM password change failed: 20, Authentication token manipulation error

actually this is because that this user’s entry is not available in /etc/passwd and /etc/shadow files, to resolve this issue you can simply add the user with same username per below command

"useradd -d /var/www/vhosts/www.domain.tld username"

and change the password once.

All resolved
