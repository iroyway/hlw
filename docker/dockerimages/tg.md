# tg镜像安装

## 安装Telegram-Cli  
### docker安装
安装镜像
```
 docker create --name telegram-cli -e TZ=Asia/Shanghai -v /root/docker:/root/.telegram-cli ugeek/telegram-cli:amd64
```
启动docer  
```
 docker start telegram-cli
```
执行telegram-cli命令行交互（先执行一次登陆，输入telegram注册的手机号码，号码记得加区号。）  
```
 docker exec -it telegram-cli telegram-cli -N -W
```
### 编译安装
克隆telegram-cli https://github.com/vysheng/tg
```
cd /root/work/telegram  ### 或者你自己想要存放的目录
git clone --recursive https://github.com/vysheng/tg.git && cd tg
```
编译安装
```
### ubuntu
sudo apt-get update
sudo apt-get -y install libreadline-dev libconfig-dev libssl-dev lua5.2 liblua5.2-dev libevent-dev libjansson-dev libpython-dev make
./configure
make
```
如出现以下错误   
![](https://raw.githubusercontent.com/iroyway/images/master/img/20210523234629.png)
解决方法：
```
apt-get install -y libgcrypt20-dev libssl-dev
./configure --disable-openssl --prefix=/usr CFLAGS="$CFLAGS -w"
make
```
申请Telegram APP Key并且登陆telegram-cli  
首先到telegram-apps(https://my.telegram.org/auth?to=apps)里申请一个telegram App key（登陆时电话号码记得加国际区号）。  
![](https://raw.githubusercontent.com/iroyway/images/master/img/20210523234830.png)
复制Public keys:
![](https://raw.githubusercontent.com/iroyway/images/master/img/20210523235007.png)
创建一个文件保存Public keys:  
```
nano /root/work/telegram/bot_key.pub
###鼠标右键粘贴
ctrl+o ##保存 按完记得敲车键
ctrl+x ##退出
```
登陆telegram-cil
```
/root/work/telegram/tg/bin/telegram-cli -k /root/work/telegram/bot_key.pub
###输入账号绑定的手机号码，记得加区号
###输入telegram App收到的验证码
```
![](https://raw.githubusercontent.com/iroyway/images/master/img/20210523235148.png)
IOS锁屏就会提示offline,打开手机telegram app就会提示online。
测试一下命令：
telegram-cil频道名称如果有空格用下划线代替。
发送命令格式/root/work/telegram/tg/bin/telegram-cli -W -e "msg 频道名称 命令"   
```
 ### 发送一条统计当前互助码池命令
 /root/work/telegram/tg/bin/telegram-cli -W -e "msg Turing_Lab_Bot /count_activity_codes"
```
回显信息比较乱，自己看手机或PC telegram APP Turing_Lab_Bot机器人 消息就好了  
## 编写脚本
### 创建一个文件，保存脚本
nano /root/docker/.telegram-cli/submit_activity_codes.sh   

### docker用户  

TuringLabbot机器人  
```
#!/bin/bash
  echo "resolve_username TuringLabbot"
(
  sleep 5
  ### @Turing_Lab_Bot
  ###京喜工厂 jxfactory
  echo "msg Turing_Lab_Bot /submit_activity_codes jxfactory 
  ###东东农场 farm
  echo "msg Turing_Lab_Bot /submit_activity_codes farm 
  ###京喜财富岛 jxcfd
  echo "msg Turing_Lab_Bot /submit_activity_codes jxcfd 
  ###东东工厂 ddfactory
  echo "msg Turing_Lab_Bot /submit_activity_codes ddfactory 
  ###种豆得豆 bean
  echo "msg Turing_Lab_Bot /submit_activity_codes bean 
  ###东东萌宠 pet
  echo "msg Turing_Lab_Bot /submit_activity_codes pet 
  echo "msg Turing_Lab_Bot /submit_activity_codes sgmh 
  ###健康社区 health
  echo "msg Turing_Lab_Bot /submit_activity_codes health 
 
  echo "safe_quit"
) | docker exec -i telegram-cli telegram-cli -N -W
```

Commit_Code_Bot 机器人
```
#!/bin/bash
  echo "resolve_username LvanLamCommitCodebot"
(
  sleep 5
 ### @Commit_Code_Bot
  ###JD签到领现金 提交助力码
  echo "msg Commit_Code_Bot /jdcash eU9YaLi7Mvgj9WuEzSFA1g&eU9Yau-xYKkgoD3UzCJH0Q&eU9Yaui6YakipGbdyyVF1g"
  ###JDCrazyjoy 提交助力码
  echo "msg Commit_Code_Bot /jdcrazyjoy Fe-hSH-WlUONQJWYYzQK1at9zd5YaBeE&pidAStt6l7-X1TaQdqIWY6t9zd5YaBeE&zP0kLlIPkhn1o5lSxHZ-Qat9zd5YaBeE"
  ###JD赚赚 提交助力码
  echo "msg Commit_Code_Bot /jdzz S5KkcREoQoVDSJB-lkqVZdA&S5KkcRh0a8wHRcUn1k6Zecw&S5KkcRhoR8gHTdRL8lKFcdA"
 
  echo "safe_quit"
) | docker exec -i telegram-cli telegram-cli -N -W
```

### 编译用户  
```
#!/bin/bash

telegramPath=TG Path #记得替换你telegram-cli目录/xxx/tg/bin

(
  echo "resolve_username TuringLabbot"
  echo "resolve_username LvanLamCommitCodebot"
  sleep 5
  ### @Turing_Lab_Bot
  ###京喜财富岛
  echo "msg Turing_Lab_Bot /submit_activity_codes jxcfd 互助码"
  ###京东闪购盲盒
  echo "msg Turing_Lab_Bot /submit_activity_codes sgmh 互助码"
  ###京东环球挑战赛
  echo "msg Turing_Lab_Bot /submit_activity_codes jdglobal 互助码"
  ###惊喜工厂
  echo "msg Turing_Lab_Bot /submit_activity_codes jxfactory 互助码"
  ###东东工厂
  echo "msg Turing_Lab_Bot /submit_activity_codes ddfactory 互助码"
  ###东东萌宠
  echo "msg Turing_Lab_Bot /submit_activity_codes pet 互助码"
  ##种豆得豆
  echo "msg Turing_Lab_Bot /submit_activity_codes bean 互助码"
  ###东东农场
  echo "msg Turing_Lab_Bot /submit_activity_codes farm 互助码"
  ### @Commit_Code_Bot
  ###JD签到领现金 提交助力码
  echo "msg Commit_Code_Bot /jdcash 互助码"
  ###JD签到领现金 提交助力码
  echo "msg Commit_Code_Bot /jdcrazyjoy 互助码"
  echo "safe_quit"
) | ${telegramPath}telegram-cli -D
```
保存脚本
```
ctrl+o ##保存 按完记得敲回车键
ctrl+x ##退出
```
```
chmod +x /root/docker/.telegram-cli/submit_activity_codes.sh
bash /root/docker/.telegram-cli/submit_activity_codes.sh
```
添加crontab定时任务  
助力池每次清空日期为每月1，8，16，24号，延迟10分钟后执行：  
```
crontab -e
10 0 1,8,16,24 * * bash /root/docker/.telegram-cli/submit_activity_codes.sh
```

本文来源于转于网络，自己学习的记录，如有侵权请联系。