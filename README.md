## Hometask #6 (10/10)

## vagrant@ubuntu2204:~$ sudo -i

## lsblk
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0                       7:0    0  63.4M  1 loop /snap/core20/1974
loop1                       7:1    0 111.9M  1 loop /snap/lxd/24322
loop2                       7:2    0  53.3M  1 loop /snap/snapd/19457
sda                         8:0    0   128G  0 disk
├─sda1                      8:1    0     1M  0 part
├─sda2                      8:2    0     2G  0 part /boot
└─sda3                      8:3    0   126G  0 part
  └─ubuntu--vg-ubuntu--lv 253:0    0    63G  0 lvm  /
sdb                         8:16   0   500M  0 disk
└─sdb1                      8:17   0   498M  0 part
  ├─vg_data-vol0          253:1    0   800M  0 lvm  /mnt/vol0
  └─vg_data-vol1          253:2    0   800M  0 lvm  /mnt/vol1
sdc                         8:32   0   600M  0 disk
└─sdc1                      8:33   0   598M  0 part
  └─vg_data-vol0          253:1    0   800M  0 lvm  /mnt/vol0
sdd                         8:48   0   400M  0 disk
└─sdd1                      8:49   0   398M  0 part
  └─vg_data-vol1          253:2    0   800M  0 lvm  /mnt/vol1
sde                         8:64   0   400M  0 disk
└─sde1                      8:65   0   398M  0 part
  └─vg_data-vol1          253:2    0   800M  0 lvm  /mnt/vol1

## df -h

Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  972K  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   62G  5.1G   54G   9% /
tmpfs                              982M     0  982M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  234M  1.6G  13% /boot
/dev/mapper/vg_data-vol0           770M   24K  714M   1% /mnt/vol0
/dev/mapper/vg_data-vol1           770M   24K  714M   1% /mnt/vol1
tmpfs                              197M  4.0K  197M   1% /run/user/1000
