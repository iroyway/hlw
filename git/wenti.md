#git常见问题解决方法
Git 冲突：commit your changes or stash them before you can merge 的解决办法

放弃本地修改，直接使用远程仓库里的最新代码（这样你可以确保你修改的代码是在别人最新的代码基础上进行的）。具体命令为：
```
git reset --hard
```

```
git pull
```
