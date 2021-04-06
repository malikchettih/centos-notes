# Create a usre for Docker


```shell
> sudo adduser docker-admin

```

```shell
> sudo passwd docker-admin

Changing password for user docker-admin.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.

```

```shell
> sudo usermod -aG docker docker-admin

```
