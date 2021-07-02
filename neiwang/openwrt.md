# openwrt 服务器版

固件下载地址：

```
https://drive.google.com/drive/folders/1dqNUrMf9n7i3y1aSh68U5Yf44WQ3KCuh
```

vps 上面搭建，脚本地址：(<https://github.com/esirplayground/VPS_OpenWrt>)

```
apt update && apt install -y wget
bash -c "$(wget -O- https://git.io/JZOn0)"
```
关闭公网  
安装软装包 
```
nginx-mod-luci
```
连接vps，修改
```
nano /etc/nginx/restrict_locally
```
nginx服务重启
```
service nginx restart
```


