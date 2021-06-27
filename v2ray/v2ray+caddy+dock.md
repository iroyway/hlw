# V2ray+Docker-compose+Caddy搭建教程
## docker安装
```
curl -sSL https://get.docker.com | bash
service docker restart
```
## docker-compose安装
```
curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
## 创建log文件同时在log目录下创建caddy和v2ray文件夹
```
mkdir -p config data /root/docker/v2ray/log/caddy /root/docker/v2ray/log/v2ray
```
## 配置V2ray配置文件config.json：
```
cat /root/docker/v2ray/config.json
```
```
{
 "log": {
  "loglevel": "warning",
  "access": "/var/log/v2ray/access.log",
  "error": "/var/log/v2ray/error.log"
 },
  "inbounds": [
    {
      "port": 端口自定义须与Caddy对应,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "UUID自行替换",
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/ray"
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```
## 配置docker-compose.yml
```
version: '3'
services:
  v2ray:
    image: v2fly/v2fly-core
    container_name: v2ray
    volumes: 
      - ./config.json:/etc/v2ray/config.json
      - ./log/v2ray:/var/log/v2ray
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    expose: 
      - "端口须与V2ray配置端口一致"
  caddy:
    image: caddy
    container_name: caddy
    volumes: 
      - ./Caddyfile:/etc/caddy/Caddyfile
      - ./data:/data
      - ./log/caddy:/var/log/caddy
      - ./config:/config
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    ports: 
      - "443:443"
```
## 创建caddyfile并配置
```
cat cat /root/docker/v2ray/caddyfile
```
```
自己的域名
{ 
  log {
    output file /var/log/caddy/caddy.log
  }
  tls 邮箱名@gmail.com
  @websockets {
    header Connection Upgrade
    header Upgrade websocket
  }
  reverse_proxy @websockets v2ray://v2ray:端口与V2ray配置信息相同
}
```
## 启动容器
docker-compose up -d

证书SSL证书评级  
https://myssl.com/