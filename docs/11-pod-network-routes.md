# Provisioning Pod Network Routes

https://github.com/kinvolk/kubernetes-the-hard-way-vagrant/blob/master/scripts/vagrant-setup-routes.bash

## Config

### worker-0

```
sudo route add -net 10.200.1.0/24 gw 192.169.33.21
```

### worker-1

```
sudo route add -net 10.200.0.0/24 gw 192.169.33.20
```

## Avant / Apres

AVANT :

```
vagrant@worker-0:~$ sudo route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         10.0.2.2        0.0.0.0         UG    0      0        0 enp0s3
10.0.2.0        0.0.0.0         255.255.255.0   U     0      0        0 enp0s3
10.200.0.0      0.0.0.0         255.255.255.0   U     0      0        0 cnio0
192.169.33.0    0.0.0.0         255.255.255.0   U     0      0        0 enp0s8
```

APRES :

```
vagrant@worker-0:~$ sudo route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         10.0.2.2        0.0.0.0         UG    0      0        0 enp0s3
10.0.2.0        0.0.0.0         255.255.255.0   U     0      0        0 enp0s3
10.200.0.0      0.0.0.0         255.255.255.0   U     0      0        0 cnio0
10.200.1.0      192.169.33.21   255.255.255.0   UG    0      0        0 enp0s8
192.169.33.0    0.0.0.0         255.255.255.0   U     0      0        0 enp0s8
```


Next: [Deploying the DNS Cluster Add-on](12-dns-addon.md)
