操作需在管理员权限下运行

卸载docker
1.删除docker的所有包

```
apt-get autoremove docker docker-ce docker-engine  docker.io  containerd runc
```

系统中可能会残留一些不再需要的 AppArmor 配置文件，执行命令sudo aa-remove-unknown 会自动扫描 AppArmor 配置文件目录，识别并删除 “未知” 的配置文件。

```
sudo aa-remove-unknown
```

2.查看docker是否卸载干净

```
dpkg -l | grep docker

dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P
```

3.删除相关插件

```
apt-get autoremove docker-ce-*
```

4.删除docker配置目录

```
rm -rf /etc/systemd/system/docker.service.d

rm -rf /var/lib/docker
```

5.确定docker卸载完毕

```
docker --version
```



