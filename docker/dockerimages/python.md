# python镜像（暂用）
dockerhub地址：nevinee/python  
基于python官方版本docker集成了bash openssl coreutils moreutils git wget curl nano tzdata perl，默认时区Asia/Shanghai。

创建：
```
docker run -dit \
  -v /宿主机上的目录/:/root \
  --name python \
  --hostname python \
  nevinee/python
```
然后进入容器，你想干啥就干啥：
```
docker exec -it python bash
```
如果映射目录下存在crontab.list，将在创建后以它作为容器的定时任务。