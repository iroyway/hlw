#  在linux中挂载u盘，设置开机启动  并将docker修改至u盘中

## 将u盘挂载
插入U盘后，使用“fdisk -l”命令  
```
fdisk -l
```
新建一个目录作为U盘的挂接点。比如说要把U盘挂载到 /mnt/usb，那么需要采用下列命令新建 /mnt/usb。v
```
mkdir /mnt/usb
```

然后就可以采用mount命令把U盘挂载在/mnt/usb。
```
mount /dev/sdb1 /mnt/usb
```
查看U盘是否成功挂载上去。



## 将u盘设置开机启动
通过blkid指令来查询uuid等信息，
```
blkid
```

我的是这样：  
>UUID="xxxx" TYPE="ext4" PARTUUID="3af27f8c-01"

```
vi /etc/fstab
```

```
UUID=“xxxx” /mnt/usb ext4 defaults,nofail 0 0
```

把UUID和TYPE填到对应位置，改成自己要挂载的路径后保存。注意：fstab是只读文件，保存和修改前要解决好权限问题。  

```
reboot
```

## 查看docker所在位置

```
docker info
```

默认情况下，Docker的存储路径都在/var/lib/docker，使用命令df -h查询占用  

```
systemctl status docker 
```

查看docker配置文件的启动目录   
方法一 直接修改/etc/docker/daemon.json配置文件，u盘我有的是ext4格式，用vfat格式没成功过

```
vi /etc/docker/daemon.json
```

```
{
  "storage-driver": "vfs",
  "registry-mirrors": ["镜像加速地址"],
  "graph": "/media/your_data_dir"
}
```

方法二 网上说的修改docker.service文件在没改u盘格式前没成功过，暂用方法一。 
最后重新加载配置文件，重新启动

```
systemctl daemon-reload
systemctl restart docker
systemctl enable docker
```
 
ok!
