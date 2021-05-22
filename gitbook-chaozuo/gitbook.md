# gitbook安装
初始化git
```
gitbook init
```
服务打开
```
gitbook serve
```
安装插件
```
gitbook install
```

## 创建仓库与分支
登陆到Github，创建一个新的仓库，名称我们就命名为book，这样我就得到一个book仓库。
克隆仓库到本地： git clone git@github.com:/USER_NAME/book.git
创建一个新分支： git checkout -b gh-pages，注意，分支名必须为gh-pages。
将分支push到仓库： git push -u origin gh-pages。
切换到主分支：git checkout master。
经过这一步处理，我们已经创建了gh-pages分支了，有了这个分支，Github会自动为你分配一个网址。

http://USERNAME.github.io/book

你可以在项目页面右下角setting中看到：

## 同步静态网站代码到分支
下面我们就可以将build好的静态网站代码同步到gh-pages分支中去了：

切换出master分支目录。我们需要将gh-pages分支内容存放在另外一个目录中
克隆gh-pages分支： 
```
git clone -b gh-pages git@github.com:USER_NAME/book.git book-end
```
这步我们只是克隆了gh-pages分支，并存放在一个新的目录book-end。
Copy静态网站到book-end目录中
Push到仓库
然后，等十来分钟后，你就可以访问到你的在线图书了。以后，只要你每次修改之后，将生成静态网站Copy到book-end目录，然后Push一下就OK了。

## 如何为目录添加序号
Gitbook默认的目录没有序号，在book.json中pluginsConfig字段添加theme-default的配置填入以下代码，增加序号，增加美观性
```
 "theme-default": {
        "showLevel": true
    },
```