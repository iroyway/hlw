# ssh连接相关操作
密钥生成
```
ssh-keygen -t rsa -f ~/.ssh/需要的名字
```

生成的这个是公钥id_rsa.pub 和 私钥 id_rsa  
你可以 ssh-keygen -f othername 来生成指定的文件名，或者生成之后 也可以两个改名  

但是ssh命令默认只会读取 id_rsa这个私钥，所以如果 是其它 的名字需要添加配置文件 ~/.ssh/config  
比如下面是我专门为 github 生成的key的配置  
```
Host github.com gist.github.com api.github.com
  HostName github.com
  IdentityFile /path/to/othername
```

