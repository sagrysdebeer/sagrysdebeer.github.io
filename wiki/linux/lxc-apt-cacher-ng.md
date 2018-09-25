---
layout: wiki
title: LXC and apt-cacher-ng
---
Install lxd and apt-cacher-ng.
Run lxd init, say yes to 'Do you want to configure the LXD bridge".
I think it will create some random local range, run:
```
ip a
```
and look for lxdbr0, unless you called it something else.


Sample output:
```
4: lxdbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 10.132.116.1/24 scope global lxdbr0
```

Change the BindAddress in /etc/apt-cacher-ng/acng.conf, to bind on that address.

```
BindAddress: 10.132.116.1
```

Restart apt-cacher-ng:

```
systemctl restart apt-cacher-ng.service
```

Double check with netstat:
```
netstat -natp
```

In whatever container you launch, and you want to use the cached packaged, remember to add
```
Acquire::http { Proxy "http://10.132.116.1:3142"; };

```

to /etc/apt/apt.conf.d/02proxy.

Don't forgot to allow the connection via ufw.
