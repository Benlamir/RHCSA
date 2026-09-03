### Lab 15.1

1. Create a 500-MB logical volume named **lvgroup**. Format it with the XFS file system and mount it persistently on /groups. Reboot your server to verify that the mount works.
    ,,,
    root@server1:~# fdisk /dev/vdb

Welcome to fdisk (util-linux 2.40.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

This disk is currently in use - repartitioning is probably a bad idea.
It's recommended to umount all file systems, and swapoff all swap
partitions on this disk.


Command (m for help): n
Partition number (2-128, default 2): 
First sector (2099200-20971486, default 2099200): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2099200-20971486, default 20969471): +1G

Created a new partition 2 of type 'Linux filesystem' and of size 1 GiB.

Command (m for help): t
Partition number (1,2, default 2): 
Partition type or alias (type L to list all): lvm

Changed type of partition 'Linux filesystem' to 'Linux LVM'.

Command (m for help): w
The partition table has been altered.
Syncing disks.
root@server1:# vgcreate vggroup1 /dev/vdb2
  Physical volume "/dev/vdb2" successfully created.
  Volume group "vggroup1" successfully created
root@server1:# vgs
  VG       #PV #LV #SN Attr   VSize    VFree   
  rhel_192   1   2   0 wz--n-  <19.00g       0 
  vggroup    1   1   0 wz--n- 1020.00m  268.00m
  vggroup1   1   0   0 wz--n- 1020.00m 1020.00m
root@server1:~# lvcreate -L +500M -n lvgroup1 /dev/vggroup1
  Logical volume "lvgroup1" created.
root@server1:# lvs
  LV       VG       Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root     rhel_192 -wi-ao---- <17.00g                                                    
  swap     rhel_192 -wi-ao----   2.00g                                                    
  lvgroup  vggroup  -wi-ao---- 752.00m                                                    
  lvgroup1 vggroup1 -wi-a----- 500.00m  
  root@server1:# mkfs.xfs /dev/vggroup1/lvgroup1
  root@server1:# mkdir /groups
  root@server1:# vim /etc/fstab
    ,,,
    /dev/vggroup1/lvgroup1 /groups xfs defaults 0 0
    ,,,
    mount -a
    findmnt --verify
    reboot
    df -h to verify that the mount is persistent


2. After rebooting, add another 250 MB to the lvgroup volume that you just created. Verify that the file system resizes as
well while resizing the volume.
    ,,,
    root@server1:~# lvextend -r -L +250M /dev/vggroup1/lvgroup1
    ,,,

3. Verify that the volume extension was successful.
    lvs to confirm the lvgroup1 has been extended


IMPORTNAT: I NEED TO REVISIT THE REDUCE SIZE METHODS!!!!!!!!!!!!
