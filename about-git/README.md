# git工具（GitHub）

↩️[返回主页]

## 1.两种方式在本地文件夹构建git环境(使用ssh连接)

具体ssh连接参照：[CSDN]

### 方式一：git clone下载Github远程仓库的完整项目，包含git环境

```sh
git clone git@github.com:xxxxx.git
```

### 方式二：在本地的文件夹中创建一个git环境（并把已有的工程同步到新建的github仓库）

Github新建一个仓库
git pull时，本地工程尽量不要有与上述新建仓库时附带的文件重名，否则可能要解决冲突
git push时，如果本地仓库和远程仓库的分支不同名，需要手动分别指定

```sh
git init
git remote add origin git@github.com:xxxxx.git
git pull origin <branch_remote>
git add .
git commit -m "first commit"
git push origin <branch_local>:<branch_remote>
git push origin <branch_same>
```

## 2.修改本地的代码

## 3.使用git管理提交版本和记录

```sh
git add .
git commit -m "提交描述"
```

## 4.将修改后的代码推送到远程仓库

```sh
git push origin <branch_local>:<branch_remote>
git push origin <branch_same>
```

## 5.特殊操作

* 查看git状态

```sh
git status
```

* 查看所有分支

```sh
git branch -a
```

* 查看当前分支

```sh
git branch
```

* 创建分支

```sh
git branch <new_branch>
```

* 切换分支

```sh
git checkout <branch_name>
```

* 使用.gitignore文件来屏蔽不需要推送至远程仓库的文件

* 取消git已经跟踪的文件

```sh
git rm -r --cached back_end/node_modules
```

* 更改远程仓库的分支名称

```sh
git branch -r
git branch -m old_branch_name new_branch_name
git push origin :old_branch_name
git push origin new_branch_name
```

[返回主页]:../README.md
[CSDN]:https://blog.csdn.net/weixin_42310154/article/details/118340458
