# 密钥连接
##1、首先在本地创建公钥和私钥
```
ssh-keygen -t rsa -f ~/.ssh/[KEY_FILENAME] -C [USERNAME]
```
[KEY_FILENAME]：您要用于 SSH 密钥文件的名称。例如，文件名 my-ssh-key 生成一个名为 my-ssh-key 的私钥文件和一个名为 my-ssh-key.pub 的公钥文件。
[USERNAME]：连接到虚拟机的用户的名称。例如 cloudysanfrancisco@gmail.com 或 cloudysanfrancisco。
详细请查看：https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys?hl=zh-cn
## 2、复制公钥
cat [KEY_FILENAME].pub
## 3、导入公钥
```
进入谷歌云平台页面 -> 计算引擎 -> 元数据 -> SSH 密钥，粘贴保存
谷歌就会把上面这段 public key 写入到 ~/.ssh/authorized_keys
```
## 4、本地通过私钥登录
finalshell 要转换格式
Termius 注意设置的时候要导入私钥
用本地终端连接
ssh -i [KEY_FILENAME] [USERNAME]@主机IP