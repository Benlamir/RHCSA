### Lab 14.1

1. Add two partitions to your server. Create both
partitions with a size of 100 MiB. One of these partitions must be
configured as swap space; the other partition must be formatted with an
Ext4 file system.
    ,,,
        student@server1:~$ lsblk
    NAME              MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sr0                11:0    1 1024M  0 rom  
    vda               252:0    0   20G  0 disk 
    ├─vda1            252:1    0    1M  0 part 
    ├─vda2            252:2    0    1G  0 part /boot
    └─vda3            252:3    0   19G  0 part 
      ├─rhel_192-root 253:0    0   17G  0 lvm  /
      └─rhel_192-swap 253:1    0    2G  0 lvm  [SWAP]
    vdb               252:16   0   10G  0 disk 

    
    root@server1:~# fdisk /dev/vdb

    Welcome to fdisk (util-linux 2.40.2).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.

    Device does not contain a recognized partition table.
    Created a new DOS (MBR) disklabel with disk identifier 0x45cc6890.

    Command (m for help): g
    Created a new GPT disklabel (GUID: 51EE356E-9B9D-4855-BF3C-B0B9931D86BA).

    Command (m for help): n
    Partition number (1-128, default 1): 
    First sector (2048-20971486, default 2048): 
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-20971486, default 20969471): +100MiB

    Created a new partition 1 of type 'Linux filesystem' and of size 100 MiB.

    Command (m for help): t
    Selected partition 1
    Partition type or alias (type L to list all): swap
    Changed type of partition 'Linux filesystem' to 'Linux swap'.

    Command (m for help): n
    Partition number (2-128, default 2): 
    First sector (206848-20971486, default 206848): 
    Last sector, +/-sectors or +/-size{K,M,G,T,P} (206848-20971486, default 20969471): +100MiB

    Created a new partition 2 of type 'Linux filesystem' and of size 100 MiB.

    Command (m for help): p
    Disk /dev/vdb: 10 GiB, 10737418240 bytes, 20971520 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: gpt
    Disk identifier: 51EE356E-9B9D-4855-BF3C-B0B9931D86BA

    Device      Start    End Sectors  Size Type
    /dev/vdb1    2048 206847  204800  100M Linux swap
    /dev/vdb2  206848 411647  204800  100M Linux filesystem

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.

    root@server1:~# mkfs.ext4 /dev/vdb2
    mke2fs 1.47.1 (20-May-2024)
    Discarding device blocks: done                            
    Creating filesystem with 102400 1k blocks and 25584 inodes
    Filesystem UUID: b12e95c1-1957-4af0-955e-c1e31d9b69a5
    Superblock backups stored on blocks: 
        8193, 24577, 40961, 57345, 73729

    Allocating group tables: done                            
    Writing inode tables: done                            
    Creating journal (4096 blocks): done
    Writing superblocks and filesystem accounting information: done 
    ,,,
2. Configure your server to automatically mount these partitions using the UUID of each. Mount the Ext4 partition on
/mounts/data and mount the swap partition as swap space.
    ,,,
    root@server1:~# mkswap /dev/vdb1
    Setting up swapspace version 1, size = 100 MiB (104853504 bytes)
    no label, UUID=c28653a6-211a-498f-a086-e05381f2b494
    root@server1: vim /etc/fstab
    UUID=c28653a6-211a-498f-a086-e05381f2b494 none swap defaults 0 0

    root@server1:mkdir -p /mounts/data

    root@server1:~# blkid | grep vdb2
    /dev/vdb2: UUID="b12e95c1-1957-4af0-955e-c1e31d9b69a5" BLOCK_SIZE="1024" TYPE="ext4" PARTUUID="c99f3ef6-6bc7-46cf-a685-9d77591c67db"
    UUID=b12e95c1-1957-4af0-955e-c1e31d9b69a5 /mounts/data ext4 defaults 0 0

    mount -a
    swapon -a
    findmnt --verify
    ,,,
3. Reboot your server and verify that all is mounted correctly. In case of problems, read Chapter 18, “Essential Troubleshooting Skills,” for tips on how to troubleshoot.
    i think he is refering to is fstab have a problem the system might not reboot
    After executing reboot (or systemctl reboot), verify that both spaces mounted automatically:

    Verify Ext4 Mount:

    Bash
    findmnt /mounts/data
    # or
    df -h /mounts/data
    Verify Swap:

    Bash
    swapon --show
    # or
    free -h
    Verify Block Devices:

    Bash
    lsblk -f /dev/vdb
    Emergency Mode Troubleshooting Tip
    If a typo ever causes the system to drop into emergency mode upon rebooting:

    Enter the root password.

    Remount the root filesystem as read-write if locked: mount -o remount,rw /

    Edit the file to fix or comment out (#) the broken line: vim /etc/fstab

    Reload systemd daemon configs: systemctl daemon-reload

    Exit or reboot: reboot
