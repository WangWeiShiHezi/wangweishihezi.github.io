登录自己的VPS，我这是Ubuntu系统

安装宝塔面板

`wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh && sudo bash install_panel.sh ed8484bec`

宝塔面板安装好以后按提示登录

一键安装 LAMP平台

在 /www/wwwroot 目录中建立一个目录  phpvod

在宝塔面板 文件 菜单中上传 下载的 phpvod.zip，然后在线解压

设置网站目录

操作步骤

网站>>设置>>网站目录，将网站目录设置为源码根目录，运行目录设置为public

添加伪静态规则
操作步骤

网站>>设置>>伪静态，复制以下规则粘贴至此处并保存。

Apache 伪静态规则

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php [L,E=PATH_INFO:$1]

```
Nginx 伪静态规则

```
if (!-e $request_filename) {
  rewrite ^/(.*)$ /index.php/$1 last;
}

```

解禁函数
操作步骤

软件商店>>PHP-x.x 设置>>禁用函数>> 删除exec、symlink


添加数据库

宝塔面板

数据库，MySql，添加数据库

数据库名  phpvod ，用户名自动建立 phpvod ，密码自动生成 ，点确认。

启动安装向导
访问 http://YOUR_DOMAIN/install/index 启动安装向导，根据向导提示完成安装。

访问 http://YOUR_DOMAIN/admin/index.html 启动后台管理