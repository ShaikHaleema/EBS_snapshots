# EBS_snapshots
voclabs:~/environment $ sudo su
[root@ip-172-31-73-224 environment]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
[root@ip-172-31-73-224 environment]# 
Broadcast message from root@ip-172-31-22-136.us-west-2.compute.internal (Fri 2024-07-26 04:50:01 UTC):

System shutdown has been cancelled


[root@ip-172-31-73-224 environment]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
xvdb      202:16   0   5G  0 disk 
[root@ip-172-31-73-224 environment]# cd ..
[root@ip-172-31-73-224 ec2-user]# ls
environment  go  node_modules  package-lock.json  package.json
[root@ip-172-31-73-224 ec2-user]# cd ..
[root@ip-172-31-73-224 home]# ls
ec2-user
[root@ip-172-31-73-224 home]# cd ..
[root@ip-172-31-73-224 /]# ls
bin  boot  dev  etc  home  lib  lib64  local  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@ip-172-31-73-224 /]# cd home
[root@ip-172-31-73-224 home]# cd ec2-user
[root@ip-172-31-73-224 ec2-user]# cd environment
[root@ip-172-31-73-224 environment]# ls
README.md
[root@ip-172-31-73-224 environment]# mkdir -p /mnt/sai
[root@ip-172-31-73-224 environment]# mkfs -t ext4 /dev/xvdb
mke2fs 1.46.5 (30-Dec-2021)
Creating filesystem with 1310720 4k blocks and 327680 inodes
Filesystem UUID: af6d07dd-b1cc-468f-977b-0ddd3e65b7fa
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 

[root@ip-172-31-73-224 environment]# mount /dev/xvdb /mnt/sai
[root@ip-172-31-73-224 environment]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
xvdb      202:16   0   5G  0 disk /mnt/sai
[root@ip-172-31-73-224 environment]# cd sai
bash: cd: sai: No such file or directory
[root@ip-172-31-73-224 environment]# cd sai
bash: cd: sai: No such file or directory
[root@ip-172-31-73-224 environment]# cd /mnt/sai
[root@ip-172-31-73-224 sai]# cat >> file1
This is file one 
^C

[*Now go back to Volumes create snapshot in the volume
and go to snapshot - create volume to the snapshot*]


[root@ip-172-31-73-224 sai]# rm file1
rm: remove regular file 'file1'? y
[root@ip-172-31-73-224 sai]# ls
lost+found
[root@ip-172-31-73-224 sai]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
xvdb      202:16   0   5G  0 disk /mnt/sai
xvdc      202:32   0   6G  0 disk 
[root@ip-172-31-73-224 sai]# mkdir -p /mnt/dir1
[root@ip-172-31-73-224 sai]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
xvdb      202:16   0   5G  0 disk /mnt/sai
xvdc      202:32   0   6G  0 disk 
[root@ip-172-31-73-224 sai]# mount /dev/xvdc /mnt/dir1
[root@ip-172-31-73-224 sai]# lsblk
NAME      MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS
xvda      202:0    0  10G  0 disk 
├─xvda1   202:1    0  10G  0 part /
├─xvda127 259:0    0   1M  0 part 
└─xvda128 259:1    0  10M  0 part /boot/efi
xvdb      202:16   0   5G  0 disk /mnt/sai
xvdc      202:32   0   6G  0 disk /mnt/dir1
[root@ip-172-31-73-224 sai]# cd /mnt/dir1
[root@ip-172-31-73-224 dir1]# ls
file1  lost+found
[root@ip-172-31-73-224 dir1]# cat file1
This is file one 
[root@ip-172-31-73-224 dir1]# cp /mnt/dir1/file1 /mnt/sai
[root@ip-172-31-73-224 dir1]# ls
file1  lost+found
[root@ip-172-31-73-224 dir1]# cd ..
[root@ip-172-31-73-224 mnt]# ls
dir1  sai
[root@ip-172-31-73-224 mnt]# cd sai
[root@ip-172-31-73-224 sai]# ls
file1  lost+found
[root@ip-172-31-73-224 sai]# cat sai
cat: sai: No such file or directory
[root@ip-172-31-73-224 sai]# cat file1
This is file one 
[root@ip-172-31-73-224 sai]# 
