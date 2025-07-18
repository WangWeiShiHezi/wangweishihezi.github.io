
```
#!/bin/bash

停止所有容器

docker stop $(docker ps -q)


删除所有容器

docker rm $(docker ps -a -q)


删除所有未被使用的镜像

docker image prune -a -f

删除所有未被使用的卷

docker volume prune -f

```


你可以将此脚本保存为 cleanup_docker.sh，然后运行它来清理Docker项目：

```
chmod +x cleanup_docker.sh

./cleanup_docker.sh

```