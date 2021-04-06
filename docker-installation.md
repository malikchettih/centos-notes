# Centos Docker installation
- https://docs.docker.com/engine/install/centos/
- https://docs.docker.com/engine/install/linux-postinstall/

```shell
> sudo yum install -y yum-utils

[sudo] password for micloud:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.crazyfrogs.org
 * extras: mirrors.standaloneinstaller.com
 * updates: centos.crazyfrogs.org
Package yum-utils-1.1.31-54.el7_8.noarch already installed and latest version
```

```shell
> sudo yum-config-manager \
>     --add-repo \
>     https://download.docker.com/linux/centos/docker-ce.repo

Loaded plugins: fastestmirror
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo

```

```shell
> sudo yum install docker-ce docker-ce-cli containerd.io

Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.crazyfrogs.org
 * extras: mirrors.standaloneinstaller.com
 * updates: centos.crazyfrogs.org
docker-ce-stable                                                                                                                                                                  | 3.5 kB  00:00:00
(1/2): docker-ce-stable/7/x86_64/updateinfo                                                                                                                                       |   55 B  00:00:00
(2/2): docker-ce-stable/7/x86_64/primary_db                                                                                                                                       |  58 kB  00:00:00
Resolving Dependencies
--> Running transaction check
---> Package containerd.io.x86_64 0:1.4.4-3.1.el7 will be installed
--> Processing Dependency: container-selinux >= 2:2.74 for package: containerd.io-1.4.4-3.1.el7.x86_64
--> Processing Dependency: libseccomp for package: containerd.io-1.4.4-3.1.el7.x86_64
---> Package docker-ce.x86_64 3:20.10.5-3.el7 will be installed
--> Processing Dependency: docker-ce-rootless-extras for package: 3:docker-ce-20.10.5-3.el7.x86_64
--> Processing Dependency: libcgroup for package: 3:docker-ce-20.10.5-3.el7.x86_64
---> Package docker-ce-cli.x86_64 1:20.10.5-3.el7 will be installed
--> Running transaction check
---> Package container-selinux.noarch 2:2.119.2-1.911c772.el7_8 will be installed
--> Processing Dependency: policycoreutils-python for package: 2:container-selinux-2.119.2-1.911c772.el7_8.noarch
---> Package docker-ce-rootless-extras.x86_64 0:20.10.5-3.el7 will be installed
--> Processing Dependency: fuse-overlayfs >= 0.7 for package: docker-ce-rootless-extras-20.10.5-3.el7.x86_64
--> Processing Dependency: slirp4netns >= 0.4 for package: docker-ce-rootless-extras-20.10.5-3.el7.x86_64
---> Package libcgroup.x86_64 0:0.41-21.el7 will be installed
---> Package libseccomp.x86_64 0:2.3.1-4.el7 will be installed
--> Running transaction check
---> Package fuse-overlayfs.x86_64 0:0.7.2-6.el7_8 will be installed
--> Processing Dependency: libfuse3.so.3(FUSE_3.2)(64bit) for package: fuse-overlayfs-0.7.2-6.el7_8.x86_64
--> Processing Dependency: libfuse3.so.3(FUSE_3.0)(64bit) for package: fuse-overlayfs-0.7.2-6.el7_8.x86_64
--> Processing Dependency: libfuse3.so.3()(64bit) for package: fuse-overlayfs-0.7.2-6.el7_8.x86_64
---> Package policycoreutils-python.x86_64 0:2.5-34.el7 will be installed
--> Processing Dependency: libsemanage-python >= 2.5-14 for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: audit-libs-python >= 2.1.3-4 for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: python-IPy for package: policycoreutils-python-2.5-34.el7.x86_64
--> Processing Dependency: checkpolicy for package: policycoreutils-python-2.5-34.el7.x86_64
---> Package slirp4netns.x86_64 0:0.4.3-4.el7_8 will be installed
--> Running transaction check
---> Package audit-libs-python.x86_64 0:2.8.5-4.el7 will be installed
---> Package checkpolicy.x86_64 0:2.5-8.el7 will be installed
---> Package fuse3-libs.x86_64 0:3.6.1-4.el7 will be installed
---> Package libsemanage-python.x86_64 0:2.5-14.el7 will be installed
---> Package python-IPy.noarch 0:0.75-6.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================
 Package                                                Arch                                Version                                                  Repository                                     Size
=========================================================================================================================================================================================================
Installing:
 containerd.io                                          x86_64                              1.4.4-3.1.el7                                            docker-ce-stable                               33 M
 docker-ce                                              x86_64                              3:20.10.5-3.el7                                          docker-ce-stable                               27 M
 docker-ce-cli                                          x86_64                              1:20.10.5-3.el7                                          docker-ce-stable                               33 M
Installing for dependencies:
 audit-libs-python                                      x86_64                              2.8.5-4.el7                                              base                                           76 k
 checkpolicy                                            x86_64                              2.5-8.el7                                                base                                          295 k
 container-selinux                                      noarch                              2:2.119.2-1.911c772.el7_8                                extras                                         40 k
 docker-ce-rootless-extras                              x86_64                              20.10.5-3.el7                                            docker-ce-stable                              9.1 M
 fuse-overlayfs                                         x86_64                              0.7.2-6.el7_8                                            extras                                         54 k
 fuse3-libs                                             x86_64                              3.6.1-4.el7                                              extras                                         82 k
 libcgroup                                              x86_64                              0.41-21.el7                                              base                                           66 k
 libseccomp                                             x86_64                              2.3.1-4.el7                                              base                                           56 k
 libsemanage-python                                     x86_64                              2.5-14.el7                                               base                                          113 k
 policycoreutils-python                                 x86_64                              2.5-34.el7                                               base                                          457 k
 python-IPy                                             noarch                              0.75-6.el7                                               base                                           32 k
 slirp4netns                                            x86_64                              0.4.3-4.el7_8                                            extras                                         81 k

Transaction Summary
=========================================================================================================================================================================================================
Install  3 Packages (+12 Dependent packages)

Total download size: 104 M
Installed size: 428 M
Is this ok [y/d/N]: y
Downloading packages:
(1/15): audit-libs-python-2.8.5-4.el7.x86_64.rpm                                                                                                                                  |  76 kB  00:00:00
(2/15): container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm                                                                                                                      |  40 kB  00:00:00
(3/15): checkpolicy-2.5-8.el7.x86_64.rpm                                                                                                                                          | 295 kB  00:00:00
warning: /var/cache/yum/x86_64/7/docker-ce-stable/packages/containerd.io-1.4.4-3.1.el7.x86_64.rpm: Header V4 RSA/SHA512 Signature, key ID 621e9f35: NOKEY              ]  0.0 B/s |  20 MB  --:--:-- ETA
Public key for containerd.io-1.4.4-3.1.el7.x86_64.rpm is not installed
(4/15): containerd.io-1.4.4-3.1.el7.x86_64.rpm                                                                                                                                    |  33 MB  00:00:00
(5/15): docker-ce-20.10.5-3.el7.x86_64.rpm                                                                                                                                        |  27 MB  00:00:00
(6/15): fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm                                                                                                                                   |  54 kB  00:00:00
(7/15): fuse3-libs-3.6.1-4.el7.x86_64.rpm                                                                                                                                         |  82 kB  00:00:00
(8/15): libsemanage-python-2.5-14.el7.x86_64.rpm                                                                                                                                  | 113 kB  00:00:00
(9/15): docker-ce-rootless-extras-20.10.5-3.el7.x86_64.rpm                                                                                                                        | 9.1 MB  00:00:00
(10/15): libcgroup-0.41-21.el7.x86_64.rpm                                                                                                                                         |  66 kB  00:00:00
(11/15): policycoreutils-python-2.5-34.el7.x86_64.rpm                                                                                                                             | 457 kB  00:00:00
(12/15): python-IPy-0.75-6.el7.noarch.rpm                                                                                                                                         |  32 kB  00:00:00
(13/15): slirp4netns-0.4.3-4.el7_8.x86_64.rpm                                                                                                                                     |  81 kB  00:00:00
(14/15): docker-ce-cli-20.10.5-3.el7.x86_64.rpm                                                                                                                                   |  33 MB  00:00:00
(15/15): libseccomp-2.3.1-4.el7.x86_64.rpm                                                                                                                                        |  56 kB  00:00:01
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     48 MB/s | 104 MB  00:00:02
Retrieving key from https://download.docker.com/linux/centos/gpg
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libseccomp-2.3.1-4.el7.x86_64                                                                                                                                                        1/15
  Installing : libcgroup-0.41-21.el7.x86_64                                                                                                                                                         2/15
  Installing : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                                                                     3/15
  Installing : audit-libs-python-2.8.5-4.el7.x86_64                                                                                                                                                 4/15
  Installing : python-IPy-0.75-6.el7.noarch                                                                                                                                                         5/15
  Installing : libsemanage-python-2.5-14.el7.x86_64                                                                                                                                                 6/15
  Installing : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                                                                        7/15
  Installing : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                                                                  8/15
  Installing : checkpolicy-2.5-8.el7.x86_64                                                                                                                                                         9/15
  Installing : policycoreutils-python-2.5-34.el7.x86_64                                                                                                                                            10/15
  Installing : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                                                                  11/15
  Installing : containerd.io-1.4.4-3.1.el7.x86_64                                                                                                                                                  12/15
  Installing : 1:docker-ce-cli-20.10.5-3.el7.x86_64                                                                                                                                                13/15
  Installing : docker-ce-rootless-extras-20.10.5-3.el7.x86_64                                                                                                                                      14/15
  Installing : 3:docker-ce-20.10.5-3.el7.x86_64                                                                                                                                                    15/15
  Verifying  : 1:docker-ce-cli-20.10.5-3.el7.x86_64                                                                                                                                                 1/15
  Verifying  : checkpolicy-2.5-8.el7.x86_64                                                                                                                                                         2/15
  Verifying  : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                                                                        3/15
  Verifying  : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                                                                  4/15
  Verifying  : libsemanage-python-2.5-14.el7.x86_64                                                                                                                                                 5/15
  Verifying  : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                                                                     6/15
  Verifying  : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                                                                   7/15
  Verifying  : python-IPy-0.75-6.el7.noarch                                                                                                                                                         8/15
  Verifying  : libseccomp-2.3.1-4.el7.x86_64                                                                                                                                                        9/15
  Verifying  : 3:docker-ce-20.10.5-3.el7.x86_64                                                                                                                                                    10/15
  Verifying  : docker-ce-rootless-extras-20.10.5-3.el7.x86_64                                                                                                                                      11/15
  Verifying  : policycoreutils-python-2.5-34.el7.x86_64                                                                                                                                            12/15
  Verifying  : containerd.io-1.4.4-3.1.el7.x86_64                                                                                                                                                  13/15
  Verifying  : audit-libs-python-2.8.5-4.el7.x86_64                                                                                                                                                14/15
  Verifying  : libcgroup-0.41-21.el7.x86_64                                                                                                                                                        15/15

Installed:
  containerd.io.x86_64 0:1.4.4-3.1.el7                                docker-ce.x86_64 3:20.10.5-3.el7                                docker-ce-cli.x86_64 1:20.10.5-3.el7

Dependency Installed:
  audit-libs-python.x86_64 0:2.8.5-4.el7     checkpolicy.x86_64 0:2.5-8.el7                 container-selinux.noarch 2:2.119.2-1.911c772.el7_8     docker-ce-rootless-extras.x86_64 0:20.10.5-3.el7
  fuse-overlayfs.x86_64 0:0.7.2-6.el7_8      fuse3-libs.x86_64 0:3.6.1-4.el7                libcgroup.x86_64 0:0.41-21.el7                         libseccomp.x86_64 0:2.3.1-4.el7
  libsemanage-python.x86_64 0:2.5-14.el7     policycoreutils-python.x86_64 0:2.5-34.el7     python-IPy.noarch 0:0.75-6.el7                         slirp4netns.x86_64 0:0.4.3-4.el7_8

Complete!
```

```shell
> sudo systemctl start docker
```

```shell
>  sudo docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

```shell
> sudo usermod -aG docker $USER
```

```shell
> sudo systemctl enable docker.service
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.

```

```shell
> sudo systemctl enable containerd.service
Created symlink from /etc/systemd/system/multi-user.target.wants/containerd.service to /usr/lib/systemd/system/containerd.service.

```
