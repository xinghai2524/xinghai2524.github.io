<h1>在Ubuntu中配置网络</h1>

`Ubuntu`使用`netplan`工具管理网络，网关配置文件位置为`/etc/netplan/50-cloud-init.yaml`

配置网关需要管理员身份

# 一    编辑配置文件

使用vim，编辑`50-cloud-init.yaml`

```yaml
network:
    ethernets:
        ens33:
            dhcp4: no
            addresses: [192.168.56.101/24]
            gateway4: 192.168.56.2
            nameservers:
                addresses: [223.5.5.5, 8.8.8.8]
    version: 2
```

其中

- ethernets的下一级为网卡名称，比如这里的ens33，使用`netplan link`或者`ip a`可以查看网卡名称
- dhcp4，表示ipv4的网络是否自动配置ip，也就是是否为动态ip
- addresses表示ip地址，这里的ip地址需要添加`子网前缀长度`用于代替子网掩码
- gateway4，表示ipv4的网关地址
- nameservers表示dns地址

配置好后保存关闭即可

# 二    应用配置

配置好后需要使用 `netplan apply`命令应用网关配置

```shell
hadoop01@hadoop01:/etc/netplan$ sudo netplan apply

** (generate:1959): WARNING **: 11:02:54.906: `gateway4` has been deprecated, use default routes instead.
See the 'Default routes' section of the documentation for more details.

** (process:1958): WARNING **: 11:02:55.474: `gateway4` has been deprecated, use default routes instead.
See the 'Default routes' section of the documentation for more details.

** (process:1958): WARNING **: 11:02:55.636: `gateway4` has been deprecated, use default routes instead.
See the 'Default routes' section of the documentation for more details.
hadoop01@hadoop01:/etc/netplan$
```

这时，可以使用`netplan status` 查看网卡信息

```shell
hadoop01@hadoop01:/etc/netplan$ netplan status
     Online state: offline
    DNS Addresses: 127.0.0.53 (stub)
       DNS Search: .

●  1: lo ethernet UNKNOWN/UP (unmanaged)
      MAC Address: 00:00:00:00:00:00
        Addresses: 127.0.0.1/8
                   ::1/128

●  2: ens33 ethernet UNKNOWN/UP (networkd: ens33)
      MAC Address: 00:0c:29:04:cc:eb (Advanced Micro Devices, Inc. [AMD])
        Addresses: 192.168.56.101/24
                   fe80::20c:29ff:fe04:cceb/64 (link)
    DNS Addresses: 223.5.5.5
                   8.8.8.8
           Routes: default via 192.168.56.2 (static)
                   192.168.56.0/24 from 192.168.56.101 (link)
                   fe80::/64 metric 256
hadoop01@hadoop01:/etc/netplan$
```

# 三    重启网络

在Ubuntu中，可以使用`systemctl restart systemd-networkd`命令重启网络

```shell
hadoop01@hadoop01:/etc/netplan$ sudo systemctl restart systemd-networkd
hadoop01@hadoop01:/etc/netplan$
```

<div style="color:red;float:right;"><sub>2025年02月09日</sub></div>
