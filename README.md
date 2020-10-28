# Allow All Squid

다 받아 주는 squid proxy

## config

``` sh
$ cat squid.conf
# https://stackoverflow.com/a/42901717
# allow all requests
acl all src 0.0.0.0/0
http_access allow all
http_access deny all
http_port 3128
coredump_dir /var/spool/squid
cache_dir ufs /var/cache/squid 100000 16 256
refresh_pattern ^ftp:		1440	20%	10080
refresh_pattern ^gopher:	1440	0%	1440
refresh_pattern -i (/cgi-bin/|\?) 0	0%	0
refresh_pattern (Release|Packages(.gz)*)$      0       20%     2880
refresh_pattern .		0	20%	4320
```

## example

``` sh
docker run --rm -d \ 
    --name squid_8444 \
    -p 3128:3128 \
    -v /tmp/cache:/var/cache/squid \
    -v /tmp/spool:/var/spool/squid \
    docker.io/leoh0/allowallsquid
```
