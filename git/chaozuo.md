#git常用操作

关联远程仓库

<!-- <table><tr><td bgcolor=Black><font color=White>git remote add origin https://github.com/iroyway/hlw.git</font></td></tr></table> 
代码颜色-->

```
git remote add origin https://github.com/iroyway/hlw.git
```
	
取消关联远程仓库
```
git remote remove origin
```

```
git branch -M master
```

```
git push -u origin master
```

查看库中的所有分支
```
git branch -v
```
建立分支并进入分支
```
git checkout -b “分支名”
```
强制更新本地文件到远程分支
```
git push origin master --force
```
1. 仅仅删除远程分支文件，不删除本地文件  
删除远程文件filename  
```
git rm --cached filename
git commit -m "delete remote file filename "
git push -u origin master(此处是当前分支的名字)
```
删除远程文件夹directoryname 
```
git rm -r --cached directoryname
git commit -m "delete remote directory directoryname "
git push -u origin master(此处是当前分支的名字)
```
2. 删除本地文件与远程分支文件
删除文件filename
```
git rm filename
git commit -m "delete file filename "
git push -u origin master(此处是当前分支的名字)
```
删除文件夹directoryname
```
git rm -r directoryname
git commit -m "delete directory directoryname "
git push -u origin master(此处是当前分支的名字)
```