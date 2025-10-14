摘要
BBR是Google开源的TCP BBR拥塞控制算法，用于提升网络连接速度，提升空间巨大，优化效果非常明显；BBR仅支持4.9以上内核Ubuntu 18.04/20.04 CentOS 8 Debian 9/10均为4.9以上内核无需更换内核可以直接开启BBR。

正文
一、使用/安装Ubuntu 20.04 Debian 9/10系统
如果你使用的是上述操作系统你可以继续跟着下面的步骤走。

二、修改系统变量

```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```

三、保存生效

```
sysctl -p
```

四、查看内核是否已开启BBR

```
sysctl net.ipv4.tcp_available_congestion_control
```

五、查看BBR是否启动

```
lsmod | grep bbr
```

显示以下即启动成功：

```
# lsmod | grep bbr
tcp_bbr                20480  14
```

完结
以上就是Ubuntu 20.04 Debian 9/10 开启Google BBR的方法的内容，欢迎小伙伴们交流讨论。