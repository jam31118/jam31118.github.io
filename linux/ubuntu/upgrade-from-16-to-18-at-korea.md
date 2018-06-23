---
layout: default
title: Upgrade from Ubuntu 16.04 to 18.04 in Korea
---

# Edit repository for good download speed

``` shell
$ NEW_DOMAIN="mirror.kakao.com"
$ OLD_DOMAIN_LIST="archive.ubuntu.com security.ubuntu.com kr.archive.ubuntu.com"
$ for OLD_DOMAIN in $OLD_DOMAIN_LIST
$ do
# 	sed -i 's/$OLD_DOMAIN/$NEW_DOMAIN/g' /etc/apt/sources.list
$ done
```

The `OLD_DOMAIN_LIST` may contain more or less, depending on your specific system
but the key point is that all relevent mirror domain should be changed to the `NEW_DOMAIN`
which is supposed to be the reasonably fast in Korea.
As of June 2018, a mirror provided by Kakao corp. is recommended with respect to its speed.
The speed typically reaches few Megabytes per second.


# Run update
At terminal,
``` shell
# do-release-upgrade -d
```


# Possible Error and Workarounds
## 'Trouble downloading packages list due to a “Hash sum mismatch” error'
Possible workaround may be found at this [askubuntu][bug-01-solution] post.

In short, combining [several answers and comments][bug-01-solution],
``` shell
# rm -rf /var/lib/apt/lists/*
# apt-get clean
# apt-get update
```
then, run again [upgrade](#run-update)


[bug-01-solution]: https://askubuntu.com/questions/41605/trouble-downloading-packages-list-due-to-a-hash-sum-mismatch-error


