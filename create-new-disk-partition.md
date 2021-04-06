# Create New partitions on added physical disk

```shell
sudo fdisk -l

Disk /dev/sdb: 268.4 GB, 268435456000 bytes, 524288000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sda: 32.2 GB, 32212254720 bytes, 62914560 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000234d9

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048     1026047      512000   83  Linux
/dev/sda2         1026048    55568383    27271168   8e  Linux LVM

Disk /dev/mapper/centos-root: 25.8 GB, 25769803776 bytes, 50331648 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/centos-swap: 2147 MB, 2147483648 bytes, 4194304 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

```

```shell
sudo df -h

Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 3.9G     0  3.9G   0% /dev
tmpfs                    3.9G     0  3.9G   0% /dev/shm
tmpfs                    3.9G  8.9M  3.9G   1% /run
tmpfs                    3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/mapper/centos-root   24G  2.4G   22G  10% /
/dev/sda1                497M  173M  324M  35% /boot
tmpfs                    783M     0  783M   0% /run/user/1000

```

```shell
sudo fdisk /dev/sdb

Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0x4d87b963.

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1):
First sector (2048-524287999, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-524287999, default 524287999): +262143999
Partition 1 of type Linux and of size 125 GiB is set

Command (m for help): t
Selected partition 1
Hex code (type L to list all codes): 8e
Changed type of partition 'Linux' to 'Linux LVM'

Command (m for help): n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): p
Partition number (2-4, default 2):
First sector (262146048-524287999, default 262146048):
Using default value 262146048
Last sector, +sectors or +size{K,M,G} (262146048-524287999, default 524287999):
Using default value 524287999
Partition 2 of type Linux and of size 125 GiB is set

Command (m for help): t
Partition number (1,2, default 2):
Hex code (type L to list all codes): 8e
Changed type of partition 'Linux' to 'Linux LVM'

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

```

```shell
sudo partprobe -s
/dev/sda: msdos partitions 1 2
/dev/sdb: msdos partitions 1 2
```
