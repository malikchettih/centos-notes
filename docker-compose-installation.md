# Docker Compose Installation

```
> sudo curl --proxy "http://150.151.144.119:3128" -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   633  100   633    0     0   2876      0 --:--:-- --:--:-- --:--:--  2890
100 12.1M  100 12.1M    0     0  21.6M      0 --:--:-- --:--:-- --:--:-- 59.8M
```

```
> sudo chmod +x /usr/local/bin/docker-compose
```

```
> docker-compose --version
docker-compose version 1.29.0, build 07737305

```

```
sudo curl --proxy "http://150.151.144.119:3128" \
    -L https://raw.githubusercontent.com/docker/compose/1.28.6/contrib/completion/bash/docker-compose \
    -o /etc/bash_completion.d/docker-compose
```

