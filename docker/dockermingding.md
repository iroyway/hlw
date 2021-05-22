# docker 命令
## docker安装命令
Docker安装

国内一键安装 
```
sudo curl -sSL https://get.daocloud.io/docker | sh
```
国外一键安装 
```
sudo curl -sSL get.docker.com | sh
```
北京外国语大学开源软件镜像站 https://mirrors.bfsu.edu.cn/help/docker-ce/  
docker-compose 安装（群晖nas docker自带安装了docker-compose）
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Ubuntu用户快速安装docker-compose
```
sudo apt-get update && sudo apt-get install -y python3-pip curl vim git moreutils
pip3 install --upgrade pip
pip install docker-compose
```
通过docker-compose version查看docker-compose版本，确认是否安装成功。
## docker常用操作命令
查看docker信息
下面jd_scripts为docker容器名字
```
docker ps -a
```
```
docker container inspect id/name
```
```
docker exec -it jd_scripts /bin/sh
```
您可以使用以下命令从主机上运行的程序中删除文件
```
docker exec <container> rm -rf <YourFile>
```
手动运行一下所有脚本  
```
docker exec -it jd_scripts /bin/sh -c 'ls jd_*.js |xargs -i node {}'
```
  
群辉docker执行下面命令  
```
docker exec -it jd_scripts /bin/sh -c 'cd /scripts;ls jd_*.js'
```
可能会用到的命令  
手动运行一脚本
```
docker exec -it jd_scripts /bin/sh -c 'git -C /scripts pull && node /scripts/jd_bean_change.js'
```
查看设置的环境变量
```
docker exec -it jd_scripts /bin/sh -c 'env'
```
查看已生效的crontab_list定时器任务
```
docker exec -it jd_scripts /bin/sh -c 'crontab -l'
```
手动更新jd_scripts仓库最新脚本
```
docker exec -it jd_scripts sh -c "docker_entrypoint.sh" 
```
仅进入容器命令
```
docker exec -it jd_scripts /bin/sh
```
删除logs文件夹里面所有的日志文件
```
rm -rf logs/*.log
```

docker portainer安装
1、安装  
先拉取最新的镜像：
```
docker pull portainer/portainer:latest
```
为Portainer创建一个volume：
```
docker volume create portainer_data
```
一条命令启动：
```
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```
注意--restart=always作用是Docker重启时，自动重启容器。
成功启动后，访问地址http://localhost:9000/就可以了。


docker portainer密码重置
1、使用如下命令获取 portainer 的名称或者 ID
```
docker ps -a
```
2、使用如下命令查看 portainer 的详细信息
```
docker inspect portainer ID
```
3、查看Hostconfig中Binds字段替换下面的portainer_data:/data字段  

4、使用 portainer 官方提供的重置密码的工具（https://github.com/portainer/helper-reset-password）
# stop the existing Portainer container
docker container stop portainer

# run the helper using the same bind-mount/volume for the data volume
docker run --rm -v portainer_data:/data portainer/helper-reset-password
2020/06/04 00:13:58 Password succesfully updated for user: admin
2020/06/04 00:13:58 Use the following password to login: &_4#\3^5V8vLTd)E"NWiJBs26G*9HPl1

# restart portainer and use the password above to login
docker container start portainer
```
