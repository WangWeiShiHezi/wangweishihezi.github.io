解决crmeb一直显示Redis扩展没有安装的问题

在使用crmeb框架时，有些用户可能会遇到一个常见问题，即Redis扩展没有安装的提示。这个问题一般是由于Redis扩展在服务器上没有安装或者没有正确配置所导致的。下面我们将介绍如何解决这个问题。

1.确认Redis扩展是否已安装

首先，我们需要确认服务器上是否已安装了Redis扩展。我们可以通过执行以下命令来检查：

```
php -m lgrep redis
```

如果输出中包含 `redis` ，则表示Redis扩展已经安装。如果输出为空，则表示Redis扩展没有安装。

2.安装Redis扩展

如果Redis扩展没有安装，我们需要先安装Redis扩展。我们可以通过以下命令来安装Redis扩展

```
pecl install redis
```

安装完成后，我们需要在 php.ini 文件中添加以下配置:

```
extension=redis.so
```

或者在宝塔面板里的 软件商店 中的 PHP 7.X  设置 ，安装扩展 ，点  pecl 安装扩展 ，输入 redis 点击安装。

安装完毕后在 配置文件 最后一行看是否写入了

```
extension=redis.so
```

3.重启Web服务器

完成以上配置后，我们需要重启Web服务器，使配置生效。可以使用以下命令来重启Apache或Nginx：

``` 
sudo systemctl restart apache2
```



```

```




```

```



```

```
