Git 小抄

如何回滚整个项目到上一版本？

```
git reset --hard HEAD^
```

如何回滚单个文件或者文件夹到指定版本

```
git checkout [<branch>] [file]
```

如何回滚单个文件或者文件夹到

```
git checkout -- [file]
```

丢弃工作区的修改

```
git checkout -- <file>
```

查看git每一次操作

```
git reflog
```
