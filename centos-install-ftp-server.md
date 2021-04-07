# Centos Firewalld activation

```
> sudo firewall-cmd --permanent --add-service=ftp
> sudo firewall-cmd --permanent --add-port=50001-50010/tcp
> sudo firewall-cmd --reload
> sudo firewall-cmd --list-all
```

```
sudo setsebool -P ftpd_full_access 1
```

```
> sudo yum install vsftpd

Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.crazyfrogs.org
 * extras: mirrors.standaloneinstaller.com
 * updates: centos.crazyfrogs.org
Resolving Dependencies
--> Running transaction check
---> Package vsftpd.x86_64 0:3.0.2-28.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================
 Package                                        Arch                                           Version                                                Repository                                    Size
=========================================================================================================================================================================================================
Installing:
 vsftpd                                         x86_64                                         3.0.2-28.el7                                           base                                         172 k

Transaction Summary
=========================================================================================================================================================================================================
Install  1 Package

Total download size: 172 k
Installed size: 353 k
Is this ok [y/d/N]: y
Downloading packages:
vsftpd-3.0.2-28.el7.x86_64.rpm                                                                                                                                                    | 172 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : vsftpd-3.0.2-28.el7.x86_64                                                                                                                                                            1/1
  Verifying  : vsftpd-3.0.2-28.el7.x86_64                                                                                                                                                            1/1

Installed:
  vsftpd.x86_64 0:3.0.2-28.el7

Complete!

```

```
> sudo mkdir -pv -m 0770 /srv/ftp/ftp_user
mkdir: created directory ‘/srv/ftp’
mkdir: created directory ‘/srv/ftp/ftp_user’

> sudo useradd -c "FTP User" -d /srv/ftp/ftp_user/ -s /sbin/nologin ftp_user
useradd: warning: the home directory already exists.
Not copying any file from skel directory into it.

> sudo chown ftp_user:ftp_user /srv/ftp/ftp_user/

> sudo passwd ftp_user
Changing password for user ftp_user.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.

```

```
```

```
```

```
```

```
```

```
```

```
```

```
```
