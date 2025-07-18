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

