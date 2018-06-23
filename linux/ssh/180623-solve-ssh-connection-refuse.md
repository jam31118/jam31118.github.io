---

layout: default
title: When facing a ssh `connection refused` error

---



# Synopsis

This error may be happen even though the ssh server didn't actually block the corresponding port nor ban your ip address etc. It can happen when you make a mistake when typing `username` in the ssh connection command. 

For example, when you want to make a ssh seesion with remote user with name `username` on a host(server) with name `hostname`, you may need a command like:

``` shell
ssh username@hostname
```

possible examples may includes:

``` shell
ssh ahn@192.168.3.104
```

where the `192.168.3.104` is the ipadress which represents the target host and the `ahn` is the username on that host.

However, you may, for some reason, confuse the username with something else, so that:

``` shell
ssh sjahn@192.168.3.104
```

You may find this mistake soon, but the problem may arise right afterward: the `connection refused` error.



# Possible Solution

```shell
ssh-keygen -f ~/.ssh/known_hosts -R hostname
```

The followings are some explanations on this command:

- `hostname` is the hostname of a target server that you've connected to. The `hostname` may be an ip address of the target server.
- `-f` option specifies a filename of the key file, which you want to modify. In this case, some of the key entries are to be deleted in `known_hosts` file, which typically reside in `~/.ssh` directory.
- `-R` option removes all keys belonging to hostname from a `known_hosts` file. In this case, the `known_hosts` file is specified by `-f` option.



Then, restarting ssh may be needed.

In Ubuntu 16.04 till 18.04, it can be done by:

``` shell
sudo systemctl restart sshd
```



After that, try ssh connection once again:

``` shell
ssh username@hostname
```

