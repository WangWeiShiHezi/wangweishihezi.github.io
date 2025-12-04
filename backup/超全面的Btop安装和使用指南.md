Btop是一个对 Linux top 命令的改进版本，提供了更丰富的功能和更好的用户体验,它不仅列出了系统的各种使用情况，包括内存、磁盘、网络和进程，还支持鼠标互动，允许用户在服务器上通过鼠标进行操作，下面我们就来看看Btop安装方法

一、Btop的魅力所在

和传统的top命令相比，它在以下几个方面表现更加出色：

全面的鼠标支持：无论是点击选中，还是滚轮翻页，都操控自如。

详尽的进程信息：一键即可展示选中「进程」的详细统计。

响应迅速、简单易用：界面美观，交互流畅，毫无上手难度。

强大的进程筛选：可以轻松过滤和查找目标进程。

直观的 I/O 监控：支持实时显示硬盘 I/O 活动与读写速度。


二、Btop安装

目前，Btop 已经进入大多数主流 Linux 发行版的官方仓库，安装也超简单：在 Ubuntu 22.04 及更高版本中，你可以使用以下命令进行安装：

````
sudo apt install btop
````

01启动Btop运行 Btop 也超简单，只需打开「终端」并执行命令：

````
btop
````

02解决No UTF-8 咯擦了detected错误

如果你在启动 btop 时，遇到以下错误提示：

````
ERROR: No UTF-8 locale detected!

Use --force-utf argument to force start if you're sure your terminal can handle it.
````

可以通过以下 2 种方法来搞定这个问题：

临时方案：附加参数强制启动：

````
btop --force-utf
````

永久方案：编辑你的~/.bashrc文件，在末尾添加这行代码：

````
export LANG=en_US.UTF-8
#保存后运行
source ~/.bashrc
````

更换主题社区为 Btop 设计了很多精美主题。下面我们就以惊艳的 Catppuccin 主题为例，教你如何换肤：

1、前往 Catppuccin 主题的发布页，下载themes.tar.gz包：

````
wget https://github.com/catppuccin/btop/releases/download/1.0.0/themes.tar.gz
````

2、解压之后，你会得到 4 种不同风格的主题：
````
tar zxvf themes.tar.gz
````

如何报错用下面命令

````
tar xvf themes.tar.gz
````

3、将.theme主题文件复制到~/.config/btop/themes目录下。

````
cp themes/*.theme ~/.config/btop/themes
````

如何报错用下面命令

````
cd ~/.config/btop/themes
cp /themes/*.* .
````

4、编辑~/.config/btop/btop.conf文件，找到color_theme = "Default"这行，改成你喜欢的主题名称，例如：
````
color_theme = "catppuccin_macchiato"
````

5、重新启动，就能看到新主题生效啦！比如我换的 Catppuccin Macchiato 风格。
