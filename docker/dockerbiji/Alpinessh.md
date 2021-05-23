# 在Alpine 中启动ssh

1. 【远程服务器】启动容器，把容器里面的22端口映射出来，例如映射到主机的3333端口：-p 3333:22  
docker-compose.yml增加  
```
Ports:
  - "3333:22"
```
2. 【远程服务器docker】设置root密码
```
sudo passwd root
```
3. 【远程服务器docker】安装ssh服务
先依次运行下列命令
```
apk add --no-cache openssh-server
apk add --no-cache sudo
apk add --no-cache openrc
rc-update add sshd
rc-status
```
4. 【远程服务器docker】在服务器上安装公钥
```
cd .ssh
cat id_rsa.pub >> authorized_keys
```
为了确保连接成功，请保证以下文件权限正确：
```
chmod 600 authorized_keys
chmod 700 ~/.ssh
```
5. 【远程服务器docker】配置ssh 开启root权限
```
sed -i "s/#PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config
sed -i "s/#PasswordAuthentication.*/PasswordAuthentication no/g" /etc/ssh/sshd_config
```
6. 【远程服务器docker】切换到root用户
```
sudo -i
```
7. 【远程服务器docker】
 ```
touch /run/openrc/softlevel
```

8. 【远程服务器docker】重启服务
```
rc-service sshd restart
```
9. 【远程服务器docker】  
看下这个ssh服务的网络连接情况:  
```
netstat -ntlp
```
如果看到如下内容,则表示已开启:  
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN 
10. 【远程服务器】连接测试
先查看服务器ip
```
docker container inspect name/id
```
![ssg1](https://raw.githubusercontent.com/iroyway/images/master/img/ssh.png)
```
ssh root@your-server-ip -A -p 22
```
11. 【本地连接】
```
ssh root@your-server-ip -A -p 3333（3333为第1步设置的端口）
```


参考：https://stackoverflow.com/questions/35690954/running-openssh-in-an-alpine-docker-container