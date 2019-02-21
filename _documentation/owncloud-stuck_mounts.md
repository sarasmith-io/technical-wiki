---
layout: default
title: "Managing External Storage mounts"
tags: ownCloud
permalink: "/documentation/managing-external-storage-mounts"
---

# Managing External Storage mounts 

Noticed an issue where External Storage folders/mounts were stuck, indicated by a spinning wheel:
![ownCloud External Storage](/assets/ownCloud-external_mounts.jpg)

External Storage configuration can be viewed and edited via the occ command via CLI on the ownCloud host. 
e.g. 
```bash
root@storage:/var/www/owncloud# sudo -u www-data php occ files_external:list user1
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+
| Mount ID | Mount Point | Storage | Authentication Type   | Configuration                                                                 | Options |
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+
| 35       | /scratch    | SFTP    | Username and password | host: "example.com", password: "***", root: "\/scratch\/user1", user: "user1" |         |
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+
root@storage:/var/www/owncloud# sudo -u www-data php occ files_external:delete 35
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+------------------+-------------------+
| Mount ID | Mount Point | Storage | Authentication Type   | Configuration                                                                 | Options | Applicable Users | Applicable Groups |
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+------------------+-------------------+
| 35       | /scratch    | SFTP    | Username and password | host: "example.com", password: "***", root: "\/scratch\/user1", user: "user1" |         | user1            |                   |
+----------+-------------+---------+-----------------------+-------------------------------------------------------------------------------+---------+------------------+-------------------+
Delete this mount? [y/N] N
```

After the deletion run a refresh with:
```bash
sudo -u www-data php occ files:scan --path="user1"
```
