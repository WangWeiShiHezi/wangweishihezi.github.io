通过命令行(CLI)设置

适用于服务器或无图形界面的环境，使用 Netplan工具。

查看网络接口名称 执行以下命令获取网络接口名称：


```
ip link show
```
编辑 Netplan 配置文件 进入 Netplan 配置目录并编辑 YAML 文件：

用 vi 或者  nano命令
```
cd /etc/netplan
sudo vi 50-cloud-init.yaml
```

应用配置并测试网络 保存文件后运行以下命令：

```
sudo netplan apply
```
注意事项

确保填写的 IP 地址、网关和 DNS 与实际网络环境匹配。

YAML 文件格式严格，请注意缩进和冒号后的空格。

如果使用 GUI 设置无效，可尝试 CLI 方法。

通过以上方法即可成功为 Ubuntu 系统设置固定 IP地址，提高网络连接的稳定性和可靠性。
