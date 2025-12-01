RustDesk 是一款开源的远程桌面工具，支持自托管服务器以提高数据安全性和连接速度。以下是通过 Docker 部署 RustDesk 私有服务器的详细步骤。

步骤 1：准备环境

确保服务器已安装 Docker 和 Docker Compose：

```
curl -fsSL https://get.docker.com | bash
sudo apt install docker-compose -y
```

确保开放以下端口： TCP: 21115, 21116, 21117, 21118, 21119 UDP: 21116

步骤 2：创建 docker-compose.yml 文件

创建项目目录并进入：

```
mkdir rustdesk-server && cd rustdesk-server
```

创建  `docker-compose.yml ` 文件：

```
nano docker-compose.yml
```

添加以下内容：


```
version: '3.8'
services:
 hbbs:
   image: rustdesk/rustdesk-server:latest
   container_name: rustdesk-hbbs
   command: hbbs -r 127.0.0.1:21117 -k _
   ports:
     - "21115:21115"
     - "21116:21116/tcp"
     - "21116:21116/udp"
     - "21118:21118"
   volumes:
     - ./data/hbbs:/root
   restart: unless-stopped
 hbbr:
   image: rustdesk/rustdesk-server:latest
   container_name: rustdesk-hbbr
   command: hbbr -k _
   ports:
     - "21117:21117"
     - "21119:21119"
   volumes:
     - ./data/hbbr:/root
   restart: unless-stopped
```

步骤 3：启动服务

拉取镜像并启动服务：

```
docker-compose pull
docker-compose up -d
```

检查服务状态：

```
docker-compose ps
```

步骤 4：获取服务器信息

获取公钥：

```
cat ./data/hbbs/id_ed25519.pub
```

配置客户端： ID服务器：<你的服务器IP>:21116 中继服务器：<你的服务器IP>:21117 服务器密钥：复制上述公钥。

将 `/rustdesk-server/data/hbbs` 目录里的 `id_ed25519` 和 `id_ed25519.pub` 两个文件或者文件内容复制到 `/rustdesk-server/data/hbbr` 目录里解决

`RustDesk reset by peer 连接被对方关闭 ` 问题。

提示与建议

定期更新服务：

```
docker-compose pull && docker-compose up -d
```

确保防火墙规则正确配置，尤其是 UDP 的 21116 端口。

如果需要支持 HTTPS，可使用 Nginx 配置反向代理。

通过以上步骤，你可以快速部署一个安全、高效的 RustDesk 私有远程桌面服务！




