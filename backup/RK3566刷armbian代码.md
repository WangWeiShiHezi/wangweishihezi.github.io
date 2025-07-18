RK3566刷armbian代码
ssh登录  用户名root  密码1234 回车
登录后会自动让修改root密码，修改成您想设置的密码即可（会让输入+确认共两次）
shell选择1回车即可
接着会让创建账号，直接按CTRL+C取消创建即可
一键换软件源命令

`bash <(curl -sSL https://linuxmirrors.cn/main.sh)`

安装casaos

`wget -qO- https://get.casaos.io | bash`

因为剩余空间不够，要选择忽略空间检查
一键docker换源

`bash <(curl -sSL https://linuxmirrors.cn/docker.sh)`

移动docker安装位置

我们把这docker的一键转移批处理下载过来，文件的全名为casaos_docker_reconfig.sh

然后上传到casaos的随便一个文件夹里

把文件所在的文件夹的路径复制出来
cd 目录
#进入批处理文件所在的目录
ls -l
#列出文件里的所有文件，检查下是否有上传上去批处理文件


确认文件已经上传了以后运行
`chmod +x casaos_docker_reconfig.sh`
`sudo ./casaos_docker_reconfig.sh`


请执行以下命令验证新配置已生效：
`docker info | grep 'Docker Root Dir'`

casaos_docker_reconfig.sh

```
#!/usr/bin/env bash
# casaos_docker_reconfig.sh
# 用途：安全停止 CasaOS 和 Docker 服务，修改 Docker 数据目录，迁移数据，重启服务
# 使用方法：
#   chmod +x casaos_docker_reconfig.sh
#   sudo ./casaos_docker_reconfig.sh

set -e
DOCKER_NEW_ROOT="/mnt/Storage1/dockerdata"
DOCKER_SERVICE_PATH="/lib/systemd/system/docker.service"
BACKUP_SUFFIX="$(date +%Y%m%d%H%M%S)"

log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $*"
}

stop_casaos_services() {
    log "Stopping CasaOS services..."
    mapfile -t services < <(systemctl list-units --type=service --all | awk '{print $1}' | grep -E '^casaos.*\\.service$' || true)
    for svc in "${services[@]}"; do
        log "Stopping $svc"
        systemctl stop "$svc" || log "Warning: Failed to stop $svc"
    done
}

stop_docker_service() {
    log "Stopping Docker service..."
    systemctl stop docker || log "Warning: Failed to stop docker"
}

modify_docker_service() {
    log "Creating new Docker data directory if not exists: $DOCKER_NEW_ROOT"
    mkdir -p "$DOCKER_NEW_ROOT"

    if [ -f "$DOCKER_SERVICE_PATH" ]; then
        log "Backing up $DOCKER_SERVICE_PATH to ${DOCKER_SERVICE_PATH}.bak.${BACKUP_SUFFIX}"
        cp "$DOCKER_SERVICE_PATH" "${DOCKER_SERVICE_PATH}.bak.${BACKUP_SUFFIX}"
        log "Modifying ExecStart to use new data root..."
        sed -i.bak "s|ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock|ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock --data-root $DOCKER_NEW_ROOT|" "$DOCKER_SERVICE_PATH"
    else
        log "Error: Docker service file not found at $DOCKER_SERVICE_PATH"
        exit 1
    fi
}

migrate_docker_data() {
    if [ -d "/var/lib/docker" ]; then
        log "Migrating Docker data to $DOCKER_NEW_ROOT using rsync..."
        rsync -avxP /var/lib/docker/ "$DOCKER_NEW_ROOT/"
        log "Data migration complete."
    else
        log "Warning: /var/lib/docker does not exist, skipping migration."
    fi
}

restart_services() {
    log "Reloading systemd daemon..."
    systemctl daemon-reload
    log "Restarting Docker..."
    systemctl restart docker
    log "Restarting CasaOS services..."
    mapfile -t services < <(systemctl list-units --type=service --all | awk '{print $1}' | grep -E '^casaos.*\\.service$' || true)
    for svc in "${services[@]}"; do
        log "Starting $svc"
        systemctl start "$svc" || log "Warning: Failed to start $svc"
    done
}

main() {
    if [ "$(id -u)" -ne 0 ]; then
        log "Error: Please run this script as root (use sudo)."
        exit 1
    fi
    stop_casaos_services
    stop_docker_service
    modify_docker_service
    migrate_docker_data
    restart_services
    log "All done. Please verify Docker root dir with: docker info | grep 'Docker Root Dir'"
}

main

```