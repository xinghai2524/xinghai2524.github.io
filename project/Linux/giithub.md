  Github一般用于Git的远程仓库，由于服务器位于国外，国内访问速度比较慢，为了提高访问速度，决定绕过DNS域名解析。

获取Github的IP地址

```
nslookup github.com
```


获取github.global.ssl.fastly.net的IP地址

```
nslookup github.global.ssl.fastly.net
```

将ip和域名写入host文件

```
sudo vim /etc/hosts
```

最后重启网络，在命令终端输入：

```
sudo systemctl restart NetworkManager
```


大功告成，赶快试试吧！
