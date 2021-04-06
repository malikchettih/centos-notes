# Centos Firewalld activation

```
> sudo systemctl status firewalld
[sudo] password for micloud:

● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
   Active: inactive (dead)
     Docs: man:firewalld(1)
```

```
> sudo systemctl enable firewalld

Created symlink from /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service to /usr/lib/systemd/system/firewalld.service.
Created symlink from /etc/systemd/system/multi-user.target.wants/firewalld.service to /usr/lib/systemd/system/firewalld.service.

```

```
> sudo systemctl start firewalld

```

```
> sudo firewall-cmd --permanent --zone=trusted --change-interface=docker0
> sudo firewall-cmd --permanent --zone=trusted --add-port=4243/tcp
> sudo firewall-cmd --zone=public --add-masquerade --permanent
> sudo firewall-cmd --reload
```
