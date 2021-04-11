```
> docker container ls
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS                      PORTS                                                                    NAMES
b06baccbeedd   oracle/database:12.2.0.1-ee   "/bin/sh -c 'exec $O…"   40 minutes ago   Up 29 minutes (unhealthy)   0.0.0.0:1521->1521/tcp, 0.0.0.0:5500->5500/tcp, 0.0.0.0:8080->8080/tcp   soe-oracle-12c-container
51e23e74d5ee   osixia/phpldapadmin:latest    "/container/tool/run"    4 days ago       Up 16 hours                 443/tcp, 0.0.0.0:6080->80/tcp                                            phpldapadmin
beff0a48f571   osixia/openldap:latest        "/container/tool/run"    4 days ago       Up 16 hours                 0.0.0.0:389->389/tcp, 0.0.0.0:636->636/tcp                               openldap


> docker container stop b06baccbeedd
> docker container rm b06baccbeedd
```

```
docker commit -a 'Malik Chettih' -m 'Udemy Soe Oracle Database container v1' b06baccbeedd malikchettih/udemy-oracle-tunning-soe-db:v1

```

```
> docker image ls

REPOSITORY                                 TAG           IMAGE ID       CREATED         SIZE
malikchettih/udemy-oracle-tunning-soe-db   v1            8fc314f4a9af   3 minutes ago   6.33GB
oracle/database                            12.2.0.1-ee   5f8e08abb5ed   11 hours ago    6GB
oraclelinux                                7-slim        c8fa2ac7772a   3 weeks ago     132MB
hello-world                                latest        d1165f221234   5 weeks ago     13.3kB
osixia/phpldapadmin                        latest        dbb580facde3   7 weeks ago     309MB
osixia/openldap                            latest        31d1d6e16394   7 weeks ago     257MB
```
