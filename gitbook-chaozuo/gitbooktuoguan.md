# 将_book发布到pages上
Pages 是github类网站提供的免费的静态网页托管服务，既然GitBook能生成基于HTTML的静态电子书籍，那自然而然，我们就会有将GitBook静态页面发布到pages服务的需求。

除了能够将书籍发布到GitBook.com外，用户还可以将电子书发布到提供Pages服务的GitHub类站点上，如国内的oschina、coding.net等等。这样做有个好处，就是访问速度比gitbook.com快很多。

这个需求情景实际上是git的应用，即将书籍的源码存放到仓库的master分支，而将书籍的html版本存放到仓库的pages分支，

## 将书籍源码托管到git远端仓库
这一环节的任务就是将书籍的源码（不含gitbook build生成的内容）推送到远端仓库。

### 新建仓库
在GitBook项目目录，如mybook中，执行如下命令，创建本地git仓库：
```
git init
```
### 添加忽略文件
使用文本编辑器，创建名为.gitignore的文件，内容如下：
```
*~
_book
.DS_Store
```
通过.gitignore文件，本地仓库将忽略临时文件和_book文件夹，达到只保存书籍源码的目的。

### 添加文件
现在可以将本地书籍源码添加到本地git仓库中了：
```
git add .
```
### 添加更新说明
```
git commit -m '更新说明文字'
```
### 建立本地仓库与远端仓库的对应关系
```
git remote add origin https://远程仓库地址.git
```
### 推送
将本地仓库内容同步到远端仓库：
```
git push -u origin master
```
至此，就完成了将gitbook源码推送到远程仓库的任务，之后书籍内容修改后，执行如下操作即可：
```
git add .
git commit -m '更新说明文字'
git push -u origin master
```
## 使用pages服务展示gitbook书籍
接下来，需要在原有本地仓库新建一个分支，在这个分支中，只保留_book文件夹中的内容，然后将这些内容推送到远程仓库的pages分支，启用pages服务，最终达到免费发布电子书的目的。

### 新建分支
```
git checkout --orphan gh-pages
```
新建名为gh-pages的分支，分支名称一定要为这个。

### 删除不需要的文件
切换到pages分支后，我们需要将_books目录之外的文件都清理掉：
```
git rm --cached -r .
git clean -df
rm -rf *~
```
### 添加忽略文件
使用文本编辑器，创建名为.gitignore的文件，内容如下：
```
*~
_book
.DS_Store
```
通过.gitignore文件，本地仓库将忽略临时文件和_book文件夹。

### 复制_book文件夹到分支根目录
```
cp -r _book/* .
```
### 添加文件
```
git add .
```
### 添加更新说明
```
git commit -m '更新说明'
```
### 推送
```
git push -u origin gh-pages
```
现在开启git托管网站的pages服务即可。

## 上述任务的自动化脚本
命令行的精髓在于可以自动执行，如下面的脚本，可以完成同时更新master分支和pages分支的目的。
```
git checkout master
git add .
git commit -m $1
git push -u origin master
git checkout gh-pages
cp -r _book/* .
git add .
git commit -m $1
git push -u origin gh-pages
git checkout master
```
在需要更新的时候，执行如下命令：
```
sh gitbook.sh '更新说明'
```