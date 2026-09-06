### Lab 16.1

1. Find out whether a new version of the kernel is available. If so, install it and reboot your computer so that it is used.
    ,,,
    root@server2:# hostnamectl status 
 Static hostname: server2.example.com
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 8322dda422c749c3893d5bd46fbfb887
         Boot ID: 79d15d7676534588b48c0b9839e98e28
    Product UUID: 4b7e67d3-5b15-4d7d-8d63-ce873b6b7e60
  Virtualization: kvm
Operating System: Red Hat Enterprise Linux 10.0 (Coughlan) 
     CPE OS Name: cpe:/o:redhat:enterprise_linux:10::baseos
          Kernel: Linux 6.12.0-55.9.1.el10_0.x86_64
    Architecture: x86-64
 Hardware Vendor: QEMU
  Hardware Model: Standard PC _Q35 + ICH9, 2009_
Firmware Version: Arch Linux 1.17.0-2-2
   Firmware Date: Tue 2014-04-01
    Firmware Age: 12y 5month 6d                            
root@server2:# dnf update kernel
Updating Subscription Management repositories.
Last metadata expiration check: 0:02:53 ago on Sun 06 Sep 2026 12:36:06 PM +01.
Dependencies resolved.
==============================================================================================
 Package              Arch    Version                   Repository                       Size
==============================================================================================
Installing:
 kernel               x86_64  6.12.0-211.51.1.el10_2    rhel-10-for-x86_64-baseos-rpms  1.6 M
Installing dependencies:
 kernel-core          x86_64  6.12.0-211.51.1.el10_2    rhel-10-for-x86_64-baseos-rpms   19 M
 kernel-modules       x86_64  6.12.0-211.51.1.el10_2    rhel-10-for-x86_64-baseos-rpms   42 M
 kernel-modules-core  x86_64  6.12.0-211.51.1.el10_2    rhel-10-for-x86_64-baseos-rpms   31 M

Transaction Summary
==============================================================================================
Install  4 Packages

Total download size: 93 M
Installed size: 136 M
Is this ok [y/N]:
,,,
2. Use the appropriate command to show recent events that have been logged by the kernel.
    ,,,
    dmesg
    ,,,
3. Locate the kernel module that is used by your
network card. Find out whether it has options. Try loading one of these
kernel module options manually; if that succeeds, take the required
measures to load this option persistently.
    ,,,
    root@server2:~# ip link show 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 52:54:00:3d:bf:12 brd ff:ff:ff:ff:ff:ff
    altname enx5254003dbf12
root@server2:~# eth
ether-wake  ethtool     
root@server2:# ethtool -i enp1s0
driver: virtio_net
version: 1.0.0
firmware-version: 
expansion-rom-version: 
bus-info: 0000:01:00.0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no
root@server2:# lsmod | grep virtio_net
virtio_net            126976  0
net_failover           24576  1 virtio_net

