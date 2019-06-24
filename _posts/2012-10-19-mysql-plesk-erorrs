---
layout: post
title: "table ‘mysql.server’ doesn’t exist error on parallels plesk"
date: 2012-10-19
---

Today I was dealing with an error while changing the password for a database user for a database using Plesk. The error was as follows

connection to the database server has failed :

Table 'mysql.server' doesn't exist

Initially i thought that we need to create that table by using

mysql > USE mysql;

mysql > CREATE TABLE `servers` ( `Server_name` char(64) NOT NULL, `Host` char(64) NOT NULL, `Db` char(64) NOT NULL, `Username` char(64) NOT NULL, `Password` char(64) NOT NULL, `Port` int(4) DEFAULT NULL, `Socket` char(64) DEFAULT NULL, `Wrapper` char(64) NOT NULL, `Owner` char(64) NOT NULL, PRIMARY KEY (`Server_name`) ) ENGINE=MyISAM DEFAULT CHARSET=utf8 COMMENT='MySQL Foreign Servers table';

But i wanna be sure before creating this table.So I investigate farther & found that this error occurs because either of compiling Mysql to new version or due to incomplete Mysql upgrade.

So we need to run mysql_fix_privilige_tables command to ensure that the mysql database will contain all the required content after any change.

So I did the following steps

root@oxygen~# mysql_fix_privilege_tables user=admin password=`cat /etc/psa/.psa.shadow` --verbose ……..output minimized ……………………….

ERROR 1061 (42000) at line 162: Duplicate key name 'Grantor'

ERROR 1054 (42S22) at line 189: Unknown column 'Type' in 'columns_priv'

ERROR 1060 (42S21) at line 211: Duplicate column name 'type'

ERROR 1060 (42S21) at line 221: Duplicate column name 'Show_db_priv'

ERROR 1060 (42S21) at line 238: Duplicate column name 'max_questions'

……..output minimized ……………………….

This resolved issue & now i am able to change the password of user through Plesk .
