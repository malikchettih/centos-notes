# Shell Proxy Setting

```
sudo vi /etc/profile.d/proxy.sh

export HTTP_PROXY=http://150.151.144.119:3128
export HTTPS_PROXY=$HTTP_PROXY
export NO_PROXY=localhost,127.0.0.1,.finastra.com,.misys.global.ad,.finastra.global,.azurecr.io,verdaccio,10.199.52.11,alm-npmjs,bm-artifacts,alm-artifacts
 
export http_proxy=$HTTP_PROXY
export https_proxy=$HTTPS_PROXY
export no_proxy=$NO_PROXY
```

# Yum Proxy Setting

```
sudo vim /etc/yum.conf

proxy=http://150.151.144.119:3128
```

# Wget Proxy Setting

```
sudo vi /etc/wgetrc

use_proxy=yes
http_proxy=http://150.151.144.119:3128
https_proxy=http://150.151.144.119:3128
```


