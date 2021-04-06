# Docker - Create a logical volume and XFS file system

- https://github.com/ibm-cloud-architecture/refarch-privatecloud/blob/master/icp-on-rhel/create-lvm-xfs.md

```shell
> sudo pvcreate /dev/sdb2
  Physical volume "/dev/sdb2" successfully created.
```

```shell
> sudo vgcreate vg_docker /dev/sdb2
  Volume group "vg_docker" successfully created

```

```shell
> sudo lvcreate --wipesignatures y -n lv_thindocker vg_docker -l 95%VG
  Logical volume "lv_thindocker" created.

```

```shell
> sudo lvcreate --wipesignatures y -n lv_thindockermeta vg_docker -l 1%VG
  Logical volume "lv_thindockermeta" created.
  
```

```shell
> sudo lvconvert -y --zero n -c 512K --thinpool vg_docker/lv_thindocker --poolmetadata vg_docker/lv_thindockermeta
  Thin pool volume with chunk size 512.00 KiB can address at most 126.50 TiB of data.
  WARNING: Converting vg_docker/lv_thindocker and vg_docker/lv_thindockermeta to thin pool's data and metadata volumes with metadata wiping.
  THIS WILL DESTROY CONTENT OF LOGICAL VOLUME (filesystem etc.)
  Converted vg_docker/lv_thindocker and vg_docker/lv_thindockermeta to thin pool.

```

```shell
> sudo vi /etc/lvm/profile/docker-thinpool.profile
 
# lvm will attempt to autoextend vg_docker/lv_thindocker
# When docker disk usage reaches 80%, lvm will attempt to add 20% more capacity.
activation {
  thin_pool_autoextend_threshold=80
  thin_pool_autoextend_percent=20
}
```

```shell
> sudo lvchange --metadataprofile docker-thinpool vg_docker/lv_thindocker
  
  Logical volume vg_docker/lv_thindocker changed.

```

```shell
> sudo mkfs.xfs -n ftype=1 /dev/vg_docker/lv_thindocker

meta-data=/dev/vg_docker/lv_thindocker isize=512    agcount=16, agsize=1945600 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=31128576, imaxpct=25
         =                       sunit=128    swidth=128 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=15200, version=2
         =                       sectsz=512   sunit=8 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0


```

```shell
> sudo mkdir -p /var/lib/docker
> sudo mount /dev/vg_docker/lv_thindocker /var/lib/docker
```

```shell
> sudo vi /etc/fstab
```

Add line 
```shell
/dev/mapper/vg_docker-lv_thindocker /var/lib/docker   xfs defaults 0 0
```
