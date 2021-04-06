# Extending /dev/mapper/centos-root on

```
sudo fdisk -l
[sudo] password for micloud:

Disk /dev/sda: 32.2 GB, 32212254720 bytes, 62914560 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000234d9

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048     1026047      512000   83  Linux
/dev/sda2         1026048    55568383    27271168   8e  Linux LVM

Disk /dev/sdb: 268.4 GB, 268435456000 bytes, 524288000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x4d87b963

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048   262146047   131072000   8e  Linux LVM
/dev/sdb2       262146048   524287999   131070976   8e  Linux LVM

Disk /dev/mapper/centos-root: 25.8 GB, 25769803776 bytes, 50331648 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/centos-swap: 2147 MB, 2147483648 bytes, 4194304 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

```
sudo pvcreate /dev/sdb1

Physical volume "/dev/sdb1" successfully created.
```

```
sudo vgextend centos /dev/sdb1

  Volume group "centos" successfully extended
```

```
sudo pvscan

  PV /dev/sda2   VG centos          lvm2 [26.00 GiB / 4.00 MiB free]
  PV /dev/sdb1   VG centos          lvm2 [<125.00 GiB / <125.00 GiB free]
  
```

```
sudo lvextend /dev/mapper/centos-root /dev/sdb1

Size of logical volume centos/root changed from 24.00 GiB (6144 extents) to <149.00 GiB (38143 extents).
Logical volume centos/root successfully resized.

```

```
sudo xfs_growfs /dev/mapper/centos-root

meta-data=/dev/mapper/centos-root isize=512    agcount=4, agsize=1572864 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0 spinodes=0
data     =                       bsize=4096   blocks=6291456, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal               bsize=4096   blocks=3072, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 6291456 to 39058432

```

```
sudo df -h

Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 3.9G     0  3.9G   0% /dev
tmpfs                    3.9G     0  3.9G   0% /dev/shm
tmpfs                    3.9G  8.9M  3.9G   1% /run
tmpfs                    3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/mapper/centos-root  149G  2.3G  147G   2% /
/dev/sda1                497M  187M  311M  38% /boot
tmpfs                    783M     0  783M   0% /run/user/1000
```
