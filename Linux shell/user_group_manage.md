
# Sample from elasticsearch user/group setting

elasticsearch 不能用 root 用户运行，那就建立一个：
[root@vcyber elasticsearch]# groupadd es
 
[root@vcyber elasticsearch]# useradd -g es es
 
[root@vcyber elasticsearch]# passwd es
 
Changing password for user es.
 
New password:
 
BAD PASSWORD: it is WAY too short
 
BAD PASSWORD: is too simple
 
Retype new password:
 
passwd: all authentication tokens updated successfully.
 
[root@vcyber elasticsearch]#
 
[root@vcyber elasticsearch]# chown -R root .
 
[root@vcyber elasticsearch]# chown -R es .
 
[root@vcyber elasticsearch]# chgrp -R es .
 
[root@vcyber elasticsearch]# ls -l
 
total 4
 
drwxr-xr-x 7 es es 4096 Mar  1 03:07 elasticsearch
 
[root@vcyber elasticsearch]#

