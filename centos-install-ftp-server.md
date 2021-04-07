# Centos vsftpd activation

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
> sudo vi vsftpd.conf

# /etc/vsftpd/vsftpd.conf
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
xferlog_std_format=YES
chroot_local_user=YES
userlist_enable=YES
userlist_deny=NO
check_shell=NO
userlist_file=/etc/vsftpd/vsftpd.user_list
allow_writeable_chroot=YES
ls_recurse_enable=YES
listen=YES
listen_ipv6=NO
pasv_enable=YES
pasv_min_port=50001
pasv_max_port=50010
pam_service_name=vsftpd
tcp_wrappers=NO
```

```
sudo vi /etc/pam.d/vsftpd

# auth required pam_shells.so
```

```
> echo ftp_user | sudo tee /etc/vsftpd/vsftpd.user_list

```

```
> sudo systemctl enable vsftpd --now
```

# Centos vsftpd sécurisationy

```
> sudo yum install epel-release mod_ssl

[sudo] password for micloud:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.crazyfrogs.org
 * extras: mirrors.standaloneinstaller.com
 * updates: centos.crazyfrogs.org
Resolving Dependencies
--> Running transaction check
---> Package epel-release.noarch 0:7-11 will be installed
---> Package mod_ssl.x86_64 1:2.4.6-97.el7.centos will be installed
--> Processing Dependency: httpd-mmn = 20120211x8664 for package: 1:mod_ssl-2.4.6-97.el7.centos.x86_64
--> Processing Dependency: httpd = 2.4.6-97.el7.centos for package: 1:mod_ssl-2.4.6-97.el7.centos.x86_64
--> Processing Dependency: httpd for package: 1:mod_ssl-2.4.6-97.el7.centos.x86_64
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-97.el7.centos will be installed
--> Processing Dependency: httpd-tools = 2.4.6-97.el7.centos for package: httpd-2.4.6-97.el7.centos.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-97.el7.centos.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.6-97.el7.centos.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.6-97.el7.centos.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.4.8-7.el7 will be installed
---> Package apr-util.x86_64 0:1.5.2-6.el7 will be installed
---> Package httpd-tools.x86_64 0:2.4.6-97.el7.centos will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================
 Package                                          Arch                                       Version                                                   Repository                                   Size
=========================================================================================================================================================================================================
Installing:
 epel-release                                     noarch                                     7-11                                                      extras                                       15 k
 mod_ssl                                          x86_64                                     1:2.4.6-97.el7.centos                                     updates                                     114 k
Installing for dependencies:
 apr                                              x86_64                                     1.4.8-7.el7                                               base                                        104 k
 apr-util                                         x86_64                                     1.5.2-6.el7                                               base                                         92 k
 httpd                                            x86_64                                     2.4.6-97.el7.centos                                       updates                                     2.7 M
 httpd-tools                                      x86_64                                     2.4.6-97.el7.centos                                       updates                                      93 k
 mailcap                                          noarch                                     2.1.41-2.el7                                              base                                         31 k

Transaction Summary
=========================================================================================================================================================================================================
Install  2 Packages (+5 Dependent packages)

Total download size: 3.2 M
Installed size: 10 M
Is this ok [y/d/N]: y
Downloading packages:
(1/7): epel-release-7-11.noarch.rpm                                                                                                                                               |  15 kB  00:00:00
(2/7): apr-util-1.5.2-6.el7.x86_64.rpm                                                                                                                                            |  92 kB  00:00:00
(3/7): apr-1.4.8-7.el7.x86_64.rpm                                                                                                                                                 | 104 kB  00:00:00
(4/7): mailcap-2.1.41-2.el7.noarch.rpm                                                                                                                                            |  31 kB  00:00:00
(5/7): httpd-tools-2.4.6-97.el7.centos.x86_64.rpm                                                                                                                                 |  93 kB  00:00:00
(6/7): mod_ssl-2.4.6-97.el7.centos.x86_64.rpm                                                                                                                                     | 114 kB  00:00:00
(7/7): httpd-2.4.6-97.el7.centos.x86_64.rpm                                                                                                                                       | 2.7 MB  00:00:00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                     10 MB/s | 3.2 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : apr-1.4.8-7.el7.x86_64                                                                                                                                                                1/7
  Installing : apr-util-1.5.2-6.el7.x86_64                                                                                                                                                           2/7
  Installing : httpd-tools-2.4.6-97.el7.centos.x86_64                                                                                                                                                3/7
  Installing : mailcap-2.1.41-2.el7.noarch                                                                                                                                                           4/7
  Installing : httpd-2.4.6-97.el7.centos.x86_64                                                                                                                                                      5/7
  Installing : 1:mod_ssl-2.4.6-97.el7.centos.x86_64                                                                                                                                                  6/7
  Installing : epel-release-7-11.noarch                                                                                                                                                              7/7
  Verifying  : epel-release-7-11.noarch                                                                                                                                                              1/7
  Verifying  : mailcap-2.1.41-2.el7.noarch                                                                                                                                                           2/7
  Verifying  : apr-1.4.8-7.el7.x86_64                                                                                                                                                                3/7
  Verifying  : apr-util-1.5.2-6.el7.x86_64                                                                                                                                                           4/7
  Verifying  : 1:mod_ssl-2.4.6-97.el7.centos.x86_64                                                                                                                                                  5/7
  Verifying  : httpd-tools-2.4.6-97.el7.centos.x86_64                                                                                                                                                6/7
  Verifying  : httpd-2.4.6-97.el7.centos.x86_64                                                                                                                                                      7/7

Installed:
  epel-release.noarch 0:7-11                                                                     mod_ssl.x86_64 1:2.4.6-97.el7.centos

Dependency Installed:
  apr.x86_64 0:1.4.8-7.el7        apr-util.x86_64 0:1.5.2-6.el7        httpd.x86_64 0:2.4.6-97.el7.centos        httpd-tools.x86_64 0:2.4.6-97.el7.centos        mailcap.noarch 0:2.1.41-2.el7

Complete!

```

```
> sudo yum install python-certbot-apache

Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
epel/x86_64/metalink                                                                                                                                                              |  28 kB  00:00:00
 * base: centos.crazyfrogs.org
 * epel: ftp.halifax.rwth-aachen.de
 * extras: mirrors.standaloneinstaller.com
 * updates: centos.crazyfrogs.org
epel                                                                                                                                                                              | 4.7 kB  00:00:00
(1/3): epel/x86_64/updateinfo                                                                                                                                                     | 1.0 MB  00:00:00
(2/3): epel/x86_64/group_gz                                                                                                                                                       |  96 kB  00:00:01
(3/3): epel/x86_64/primary_db                                                                                                                                                     | 6.9 MB  00:00:13
Resolving Dependencies
--> Running transaction check
---> Package python2-certbot-apache.noarch 0:1.11.0-1.el7 will be installed
--> Processing Dependency: certbot >= 0.39.0 for package: python2-certbot-apache-1.11.0-1.el7.noarch
--> Processing Dependency: python2-acme >= 0.29.0 for package: python2-certbot-apache-1.11.0-1.el7.noarch
--> Processing Dependency: python2-certbot >= 1.6.0 for package: python2-certbot-apache-1.11.0-1.el7.noarch
--> Processing Dependency: python-augeas for package: python2-certbot-apache-1.11.0-1.el7.noarch
--> Running transaction check
---> Package certbot.noarch 0:1.11.0-1.el7 will be installed
---> Package python-augeas.noarch 0:0.5.0-2.el7 will be installed
--> Processing Dependency: augeas-libs for package: python-augeas-0.5.0-2.el7.noarch
---> Package python2-acme.noarch 0:1.11.0-1.el7 will be installed
--> Processing Dependency: pyOpenSSL >= 0.13.1 for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-josepy >= 1.1.0 for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-requests >= 2.6.0 for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python-ndg_httpsclient for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python-requests-toolbelt for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-cryptography for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-pyasn1 for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-pyrfc3339 for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: python2-six for package: python2-acme-1.11.0-1.el7.noarch
--> Processing Dependency: pytz for package: python2-acme-1.11.0-1.el7.noarch
---> Package python2-certbot.noarch 0:1.11.0-1.el7 will be installed
--> Processing Dependency: python-parsedatetime >= 1.3 for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python2-configargparse >= 0.9.3 for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python2-distro >= 1.0.1 for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python-setuptools for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python-zope-component for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python-zope-interface for package: python2-certbot-1.11.0-1.el7.noarch
--> Processing Dependency: python2-mock for package: python2-certbot-1.11.0-1.el7.noarch
--> Running transaction check
---> Package augeas-libs.x86_64 0:1.4.0-10.el7 will be installed
---> Package pyOpenSSL.x86_64 0:0.13.1-4.el7 will be installed
---> Package python-ndg_httpsclient.noarch 0:0.3.2-1.el7 will be installed
---> Package python-requests.noarch 0:2.6.0-10.el7 will be installed
--> Processing Dependency: python-urllib3 >= 1.10.2-1 for package: python-requests-2.6.0-10.el7.noarch
---> Package python-requests-toolbelt.noarch 0:0.8.0-3.el7 will be installed
---> Package python-setuptools.noarch 0:0.9.8-7.el7 will be installed
--> Processing Dependency: python-backports-ssl_match_hostname for package: python-setuptools-0.9.8-7.el7.noarch
---> Package python-zope-component.noarch 1:4.1.0-5.el7 will be installed
--> Processing Dependency: python-zope-event for package: 1:python-zope-component-4.1.0-5.el7.noarch
---> Package python-zope-interface.x86_64 0:4.0.5-4.el7 will be installed
---> Package python2-configargparse.noarch 0:0.11.0-2.el7 will be installed
---> Package python2-cryptography.x86_64 0:1.7.2-2.el7 will be installed
--> Processing Dependency: python-six >= 1.4.1 for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-idna >= 2.0 for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-cffi >= 1.4.1 for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-ipaddress for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-enum34 for package: python2-cryptography-1.7.2-2.el7.x86_64
---> Package python2-distro.noarch 0:1.2.0-3.el7 will be installed
---> Package python2-josepy.noarch 0:1.3.0-2.el7 will be installed
---> Package python2-mock.noarch 0:1.0.1-10.el7 will be installed
---> Package python2-parsedatetime.noarch 0:2.4-6.el7 will be installed
--> Processing Dependency: python2-future for package: python2-parsedatetime-2.4-6.el7.noarch
---> Package python2-pyasn1.noarch 0:0.1.9-7.el7 will be installed
---> Package python2-pyrfc3339.noarch 0:1.1-3.el7 will be installed
---> Package python2-six.noarch 0:1.9.0-0.el7 will be installed
---> Package pytz.noarch 0:2016.10-2.el7 will be installed
--> Running transaction check
---> Package python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7 will be installed
--> Processing Dependency: python-backports for package: python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch
---> Package python-cffi.x86_64 0:1.6.0-5.el7 will be installed
--> Processing Dependency: python-pycparser for package: python-cffi-1.6.0-5.el7.x86_64
---> Package python-enum34.noarch 0:1.0.4-1.el7 will be installed
---> Package python-idna.noarch 0:2.4-1.el7 will be installed
---> Package python-ipaddress.noarch 0:1.0.16-2.el7 will be installed
---> Package python-six.noarch 0:1.9.0-2.el7 will be installed
---> Package python-urllib3.noarch 0:1.10.2-7.el7 will be installed
---> Package python-zope-event.noarch 0:4.0.3-2.el7 will be installed
---> Package python2-future.noarch 0:0.18.2-2.el7 will be installed
--> Running transaction check
---> Package python-backports.x86_64 0:1.0-8.el7 will be installed
---> Package python-pycparser.noarch 0:2.14-1.el7 will be installed
--> Processing Dependency: python-ply for package: python-pycparser-2.14-1.el7.noarch
--> Running transaction check
---> Package python-ply.noarch 0:3.4-11.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================================================================================================================
 Package                                                              Arch                                    Version                                        Repository                             Size
=========================================================================================================================================================================================================
Installing:
 python2-certbot-apache                                               noarch                                  1.11.0-1.el7                                   epel                                  139 k
Installing for dependencies:
 augeas-libs                                                          x86_64                                  1.4.0-10.el7                                   base                                  357 k
 certbot                                                              noarch                                  1.11.0-1.el7                                   epel                                   46 k
 pyOpenSSL                                                            x86_64                                  0.13.1-4.el7                                   base                                  135 k
 python-augeas                                                        noarch                                  0.5.0-2.el7                                    base                                   25 k
 python-backports                                                     x86_64                                  1.0-8.el7                                      base                                  5.8 k
 python-backports-ssl_match_hostname                                  noarch                                  3.5.0.1-1.el7                                  base                                   13 k
 python-cffi                                                          x86_64                                  1.6.0-5.el7                                    base                                  218 k
 python-enum34                                                        noarch                                  1.0.4-1.el7                                    base                                   52 k
 python-idna                                                          noarch                                  2.4-1.el7                                      base                                   94 k
 python-ipaddress                                                     noarch                                  1.0.16-2.el7                                   base                                   34 k
 python-ndg_httpsclient                                               noarch                                  0.3.2-1.el7                                    epel                                   43 k
 python-ply                                                           noarch                                  3.4-11.el7                                     base                                  123 k
 python-pycparser                                                     noarch                                  2.14-1.el7                                     base                                  104 k
 python-requests                                                      noarch                                  2.6.0-10.el7                                   base                                   95 k
 python-requests-toolbelt                                             noarch                                  0.8.0-3.el7                                    epel                                   78 k
 python-setuptools                                                    noarch                                  0.9.8-7.el7                                    base                                  397 k
 python-six                                                           noarch                                  1.9.0-2.el7                                    base                                   29 k
 python-urllib3                                                       noarch                                  1.10.2-7.el7                                   base                                  103 k
 python-zope-component                                                noarch                                  1:4.1.0-5.el7                                  epel                                  228 k
 python-zope-event                                                    noarch                                  4.0.3-2.el7                                    epel                                   79 k
 python-zope-interface                                                x86_64                                  4.0.5-4.el7                                    base                                  138 k
 python2-acme                                                         noarch                                  1.11.0-1.el7                                   epel                                   83 k
 python2-certbot                                                      noarch                                  1.11.0-1.el7                                   epel                                  386 k
 python2-configargparse                                               noarch                                  0.11.0-2.el7                                   epel                                   31 k
 python2-cryptography                                                 x86_64                                  1.7.2-2.el7                                    base                                  502 k
 python2-distro                                                       noarch                                  1.2.0-3.el7                                    epel                                   29 k
 python2-future                                                       noarch                                  0.18.2-2.el7                                   epel                                  806 k
 python2-josepy                                                       noarch                                  1.3.0-2.el7                                    epel                                   89 k
 python2-mock                                                         noarch                                  1.0.1-10.el7                                   epel                                   92 k
 python2-parsedatetime                                                noarch                                  2.4-6.el7                                      epel                                   78 k
 python2-pyasn1                                                       noarch                                  0.1.9-7.el7                                    base                                  100 k
 python2-pyrfc3339                                                    noarch                                  1.1-3.el7                                      epel                                   16 k
 python2-six                                                          noarch                                  1.9.0-0.el7                                    epel                                  2.9 k
 pytz                                                                 noarch                                  2016.10-2.el7                                  base                                   46 k

Transaction Summary
=========================================================================================================================================================================================================
Install  1 Package (+34 Dependent packages)

Total download size: 4.7 M
Installed size: 21 M
Is this ok [y/d/N]: y
Downloading packages:
(1/35): pyOpenSSL-0.13.1-4.el7.x86_64.rpm                                                                                                                                         | 135 kB  00:00:00
(2/35): augeas-libs-1.4.0-10.el7.x86_64.rpm                                                                                                                                       | 357 kB  00:00:00
(3/35): python-augeas-0.5.0-2.el7.noarch.rpm                                                                                                                                      |  25 kB  00:00:00
(4/35): python-backports-1.0-8.el7.x86_64.rpm                                                                                                                                     | 5.8 kB  00:00:00
(5/35): python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch.rpm                                                                                                              |  13 kB  00:00:00
(6/35): python-enum34-1.0.4-1.el7.noarch.rpm                                                                                                                                      |  52 kB  00:00:00
(7/35): python-cffi-1.6.0-5.el7.x86_64.rpm                                                                                                                                        | 218 kB  00:00:00
(8/35): python-idna-2.4-1.el7.noarch.rpm                                                                                                                                          |  94 kB  00:00:00
(9/35): python-ipaddress-1.0.16-2.el7.noarch.rpm                                                                                                                                  |  34 kB  00:00:00
(10/35): python-ply-3.4-11.el7.noarch.rpm                                                                                                                                         | 123 kB  00:00:00
(11/35): python-pycparser-2.14-1.el7.noarch.rpm                                                                                                                                   | 104 kB  00:00:00
(12/35): python-requests-2.6.0-10.el7.noarch.rpm                                                                                                                                  |  95 kB  00:00:00
(13/35): python-six-1.9.0-2.el7.noarch.rpm                                                                                                                                        |  29 kB  00:00:00
(14/35): python-urllib3-1.10.2-7.el7.noarch.rpm                                                                                                                                   | 103 kB  00:00:00
(15/35): python-setuptools-0.9.8-7.el7.noarch.rpm                                                                                                                                 | 397 kB  00:00:00
warning: /var/cache/yum/x86_64/7/epel/packages/python-ndg_httpsclient-0.3.2-1.el7.noarch.rpm: Header V3 RSA/SHA256 Signature, key ID 352c64e5: NOKEY
Public key for python-ndg_httpsclient-0.3.2-1.el7.noarch.rpm is not installed
(16/35): python-ndg_httpsclient-0.3.2-1.el7.noarch.rpm                                                                                                                            |  43 kB  00:00:00
(17/35): python-zope-interface-4.0.5-4.el7.x86_64.rpm                                                                                                                             | 138 kB  00:00:00
(18/35): python2-acme-1.11.0-1.el7.noarch.rpm                                                                                                                                     |  83 kB  00:00:00
(19/35): python-requests-toolbelt-0.8.0-3.el7.noarch.rpm                                                                                                                          |  78 kB  00:00:00
(20/35): certbot-1.11.0-1.el7.noarch.rpm                                                                                                                                          |  46 kB  00:00:00
(21/35): python2-certbot-1.11.0-1.el7.noarch.rpm                                                                                                                                  | 386 kB  00:00:00
(22/35): python2-configargparse-0.11.0-2.el7.noarch.rpm                                                                                                                           |  31 kB  00:00:00
(23/35): python2-certbot-apache-1.11.0-1.el7.noarch.rpm                                                                                                                           | 139 kB  00:00:00
(24/35): python2-distro-1.2.0-3.el7.noarch.rpm                                                                                                                                    |  29 kB  00:00:00
(25/35): python2-cryptography-1.7.2-2.el7.x86_64.rpm                                                                                                                              | 502 kB  00:00:00
(26/35): python2-josepy-1.3.0-2.el7.noarch.rpm                                                                                                                                    |  89 kB  00:00:00
(27/35): python-zope-event-4.0.3-2.el7.noarch.rpm                                                                                                                                 |  79 kB  00:00:00
(28/35): python-zope-component-4.1.0-5.el7.noarch.rpm                                                                                                                             | 228 kB  00:00:00
(29/35): python2-pyasn1-0.1.9-7.el7.noarch.rpm                                                                                                                                    | 100 kB  00:00:00
(30/35): python2-parsedatetime-2.4-6.el7.noarch.rpm                                                                                                                               |  78 kB  00:00:00
(31/35): python2-mock-1.0.1-10.el7.noarch.rpm                                                                                                                                     |  92 kB  00:00:00
(32/35): pytz-2016.10-2.el7.noarch.rpm                                                                                                                                            |  46 kB  00:00:00
(33/35): python2-future-0.18.2-2.el7.noarch.rpm                                                                                                                                   | 806 kB  00:00:00
(34/35): python2-six-1.9.0-0.el7.noarch.rpm                                                                                                                                       | 2.9 kB  00:00:00
(35/35): python2-pyrfc3339-1.1-3.el7.noarch.rpm                                                                                                                                   |  16 kB  00:00:00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                    6.2 MB/s | 4.7 MB  00:00:00
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Importing GPG key 0x352C64E5:
 Userid     : "Fedora EPEL (7) <epel@fedoraproject.org>"
 Fingerprint: 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5
 Package    : epel-release-7-11.noarch (@extras)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : python-ipaddress-1.0.16-2.el7.noarch                                                                                                                                                 1/35
  Installing : python2-pyasn1-0.1.9-7.el7.noarch                                                                                                                                                    2/35
  Installing : pyOpenSSL-0.13.1-4.el7.x86_64                                                                                                                                                        3/35
  Installing : python-six-1.9.0-2.el7.noarch                                                                                                                                                        4/35
  Installing : python2-six-1.9.0-0.el7.noarch                                                                                                                                                       5/35
  Installing : python2-pyrfc3339-1.1-3.el7.noarch                                                                                                                                                   6/35
  Installing : python-zope-interface-4.0.5-4.el7.x86_64                                                                                                                                             7/35
  Installing : pytz-2016.10-2.el7.noarch                                                                                                                                                            8/35
  Installing : python-zope-event-4.0.3-2.el7.noarch                                                                                                                                                 9/35
  Installing : 1:python-zope-component-4.1.0-5.el7.noarch                                                                                                                                          10/35
  Installing : python2-mock-1.0.1-10.el7.noarch                                                                                                                                                    11/35
  Installing : python-backports-1.0-8.el7.x86_64                                                                                                                                                   12/35
  Installing : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                                                                                            13/35
  Installing : python-setuptools-0.9.8-7.el7.noarch                                                                                                                                                14/35
  Installing : python-ndg_httpsclient-0.3.2-1.el7.noarch                                                                                                                                           15/35
  Installing : python-urllib3-1.10.2-7.el7.noarch                                                                                                                                                  16/35
  Installing : python-requests-2.6.0-10.el7.noarch                                                                                                                                                 17/35
  Installing : python-requests-toolbelt-0.8.0-3.el7.noarch                                                                                                                                         18/35
  Installing : python-ply-3.4-11.el7.noarch                                                                                                                                                        19/35
  Installing : python-pycparser-2.14-1.el7.noarch                                                                                                                                                  20/35
  Installing : python-cffi-1.6.0-5.el7.x86_64                                                                                                                                                      21/35
  Installing : python2-distro-1.2.0-3.el7.noarch                                                                                                                                                   22/35
  Installing : python-idna-2.4-1.el7.noarch                                                                                                                                                        23/35
  Installing : python2-future-0.18.2-2.el7.noarch                                                                                                                                                  24/35
  Installing : python2-parsedatetime-2.4-6.el7.noarch                                                                                                                                              25/35
  Installing : python2-configargparse-0.11.0-2.el7.noarch                                                                                                                                          26/35
  Installing : python-enum34-1.0.4-1.el7.noarch                                                                                                                                                    27/35
  Installing : python2-cryptography-1.7.2-2.el7.x86_64                                                                                                                                             28/35
  Installing : python2-josepy-1.3.0-2.el7.noarch                                                                                                                                                   29/35
  Installing : python2-acme-1.11.0-1.el7.noarch                                                                                                                                                    30/35
  Installing : python2-certbot-1.11.0-1.el7.noarch                                                                                                                                                 31/35
  Installing : certbot-1.11.0-1.el7.noarch                                                                                                                                                         32/35
  Installing : augeas-libs-1.4.0-10.el7.x86_64                                                                                                                                                     33/35
  Installing : python-augeas-0.5.0-2.el7.noarch                                                                                                                                                    34/35
  Installing : python2-certbot-apache-1.11.0-1.el7.noarch                                                                                                                                          35/35
  Verifying  : python-augeas-0.5.0-2.el7.noarch                                                                                                                                                     1/35
  Verifying  : augeas-libs-1.4.0-10.el7.x86_64                                                                                                                                                      2/35
  Verifying  : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                                                                                             3/35
  Verifying  : python2-six-1.9.0-0.el7.noarch                                                                                                                                                       4/35
  Verifying  : pytz-2016.10-2.el7.noarch                                                                                                                                                            5/35
  Verifying  : python-ndg_httpsclient-0.3.2-1.el7.noarch                                                                                                                                            6/35
  Verifying  : python-enum34-1.0.4-1.el7.noarch                                                                                                                                                     7/35
  Verifying  : 1:python-zope-component-4.1.0-5.el7.noarch                                                                                                                                           8/35
  Verifying  : python2-certbot-apache-1.11.0-1.el7.noarch                                                                                                                                           9/35
  Verifying  : python-setuptools-0.9.8-7.el7.noarch                                                                                                                                                10/35
  Verifying  : python-urllib3-1.10.2-7.el7.noarch                                                                                                                                                  11/35
  Verifying  : certbot-1.11.0-1.el7.noarch                                                                                                                                                         12/35
  Verifying  : python-requests-toolbelt-0.8.0-3.el7.noarch                                                                                                                                         13/35
  Verifying  : python2-configargparse-0.11.0-2.el7.noarch                                                                                                                                          14/35
  Verifying  : python2-future-0.18.2-2.el7.noarch                                                                                                                                                  15/35
  Verifying  : python-zope-interface-4.0.5-4.el7.x86_64                                                                                                                                            16/35
  Verifying  : python-six-1.9.0-2.el7.noarch                                                                                                                                                       17/35
  Verifying  : python-idna-2.4-1.el7.noarch                                                                                                                                                        18/35
  Verifying  : python2-distro-1.2.0-3.el7.noarch                                                                                                                                                   19/35
  Verifying  : python2-josepy-1.3.0-2.el7.noarch                                                                                                                                                   20/35
  Verifying  : python-ply-3.4-11.el7.noarch                                                                                                                                                        21/35
  Verifying  : python-backports-1.0-8.el7.x86_64                                                                                                                                                   22/35
  Verifying  : python2-acme-1.11.0-1.el7.noarch                                                                                                                                                    23/35
  Verifying  : pyOpenSSL-0.13.1-4.el7.x86_64                                                                                                                                                       24/35
  Verifying  : python-cffi-1.6.0-5.el7.x86_64                                                                                                                                                      25/35
  Verifying  : python2-mock-1.0.1-10.el7.noarch                                                                                                                                                    26/35
  Verifying  : python-pycparser-2.14-1.el7.noarch                                                                                                                                                  27/35
  Verifying  : python-requests-2.6.0-10.el7.noarch                                                                                                                                                 28/35
  Verifying  : python-zope-event-4.0.3-2.el7.noarch                                                                                                                                                29/35
  Verifying  : python2-pyrfc3339-1.1-3.el7.noarch                                                                                                                                                  30/35
  Verifying  : python2-pyasn1-0.1.9-7.el7.noarch                                                                                                                                                   31/35
  Verifying  : python-ipaddress-1.0.16-2.el7.noarch                                                                                                                                                32/35
  Verifying  : python2-parsedatetime-2.4-6.el7.noarch                                                                                                                                              33/35
  Verifying  : python2-cryptography-1.7.2-2.el7.x86_64                                                                                                                                             34/35
  Verifying  : python2-certbot-1.11.0-1.el7.noarch                                                                                                                                                 35/35

Installed:
  python2-certbot-apache.noarch 0:1.11.0-1.el7

Dependency Installed:
  augeas-libs.x86_64 0:1.4.0-10.el7           certbot.noarch 0:1.11.0-1.el7                               pyOpenSSL.x86_64 0:0.13.1-4.el7                python-augeas.noarch 0:0.5.0-2.el7
  python-backports.x86_64 0:1.0-8.el7         python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7  python-cffi.x86_64 0:1.6.0-5.el7               python-enum34.noarch 0:1.0.4-1.el7
  python-idna.noarch 0:2.4-1.el7              python-ipaddress.noarch 0:1.0.16-2.el7                      python-ndg_httpsclient.noarch 0:0.3.2-1.el7    python-ply.noarch 0:3.4-11.el7
  python-pycparser.noarch 0:2.14-1.el7        python-requests.noarch 0:2.6.0-10.el7                       python-requests-toolbelt.noarch 0:0.8.0-3.el7  python-setuptools.noarch 0:0.9.8-7.el7
  python-six.noarch 0:1.9.0-2.el7             python-urllib3.noarch 0:1.10.2-7.el7                        python-zope-component.noarch 1:4.1.0-5.el7     python-zope-event.noarch 0:4.0.3-2.el7
  python-zope-interface.x86_64 0:4.0.5-4.el7  python2-acme.noarch 0:1.11.0-1.el7                          python2-certbot.noarch 0:1.11.0-1.el7          python2-configargparse.noarch 0:0.11.0-2.el7
  python2-cryptography.x86_64 0:1.7.2-2.el7   python2-distro.noarch 0:1.2.0-3.el7                         python2-future.noarch 0:0.18.2-2.el7           python2-josepy.noarch 0:1.3.0-2.el7
  python2-mock.noarch 0:1.0.1-10.el7          python2-parsedatetime.noarch 0:2.4-6.el7                    python2-pyasn1.noarch 0:0.1.9-7.el7            python2-pyrfc3339.noarch 0:1.1-3.el7
  python2-six.noarch 0:1.9.0-0.el7            pytz.noarch 0:2016.10-2.el7

Complete!

```

```
> sudo mkdir -pv -m 0770 /srv/ssl/vsftpd-certificats

```

```
> sudo certbot certonly --non-interactive --email info@FR1SLPSKTP00325.misys.global.ad \
  --preferred-challenges http --standalone --agree-tos --renew-by-default \
  --webroot-path /srv/ssl/vsftpd-certificats -d FR1SLPSKTP00325.misys.global.ad -d FR1SLPSKTP00325.misys.global.ad --dry-run
```

```
```
