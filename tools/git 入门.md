# git 入门

> [来源](http://blog.csdn.net/column/details/13170.html)
>
> by: bubao
>
> 创建时间:2017-03-10 14:22:51
>
> 地址: 湛江

### 准备工作

`mkdir test` 

创建文件夹 test

`cd test` 

切换到 test 目录

`touch a.md` 

新建 a.md 文件

### 查看状态

`git status`

### 初始化git库

`git init` 

### 提交到git「暂存区」

`git add`

### 提交到git 仓库

`git commit -m "first"`

commit 是提交的意思，-m 代表是提交信息

### 日志

`git log` 

### 创建分支

`git branch a` 

创建一个分支a，这时候分支 a 跟分支 master 是一模一样的内容

### 切换分支

`git checkout a` 

切换到分支a

`git checkout -b a`

新建一个a分支，并且自动切换到a分支。

### 合并分支

先切换到master 分支，把a分支的代码合并过来

`git merge a`  

### 删除分支

`git branch -d a`

### 查看远程分支列表

`git branch -r`

### 强制删除分支

有些时候可能会删除失败，比如如果a分支的代码还没有合并到master，你执行 `git branch -d a` 是删除不了的，它会智能的提示你a分支还有未合并的代码，但是如果你非要删除，那就执行 `git branch -D a `就可以强制删除a分支。

`git branch -D a` 

### 版本标签

**创建tag**

`git tag v1.0`

**查看tag**

` git tag`

**切换tag**

`git checkout v1.0`

## Github

### 生成SSH

`ssh-keygen -t rsa`

指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 `id_rsa` 和 `id_rsa.pub` ，而 `id_rsa` 是密钥，`id_rsa.pub` 就是公钥。把 `id_rsa.pub` 的内容添加到 GitHub 上，这样你本地的 `id_rsa` 密钥跟 GitHub 上的 `id_rsa.pub` 公钥进行配对，授权成功才可以提交代码。

### 查看公钥

```shell
cd ~/.ssh
cat id_rsa.pub
```

### 测试SSH key

```shell
▶  ssh -T git@github.com
Hi bubao! You've successfully authenticated, but GitHub does not provide shell access.
```

### 设置用户名和用户邮箱

```shell
git config —global user.name "bubao"
git config —global user.email "asd565586630@gmail.com"
```

### Push & Pull

`git push origin master`

把本地代码推到远程 master 分支

`git pull origin master`

把远程最新的代码更新到本地。一般在 push 之前都会先 pull ，这样不容易冲突。

### 关联本地已有项目

`git remote add 远程仓库名字 github地址`

### 查看当前项目有哪些远程仓库

`git remote -v`

### alias

```
git config --global alias.co checkout  # 别名
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.psm 'push origin master'
git config --global alias.plm 'pull origin master'
git config --global alias.lg 'log –graph –pretty=format:’%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset’ –abbrev-commit –date=relative'
```

### 其他配置

`git config --global core.editor "vim"  # 设置Editor使用vim`

`git config --global color.ui true #给 Git 着色`

`git config --global core.quotepath false # 设置显示中文文件名`

> 默认这些配置都在 **~/.gitconfig** 文件下的，你可以找到这个文件查看自己的配置，也可以输入 **git config -l** 命令查看。

### diff

`git diff #查看修改变动`

> 直接输入 **git diff** 只能比较当前文件和暂存区文件差异，什么是暂存区？就是你还没有执行 **git add** 的文件。

### stash

把当前分支所有没有 commit 的代码先暂存起来：

`git stash`

暂存区记录：

`git stash list`

暂存区代码还原：

`git stash apply`

清除暂存区记录：

`git stash drop`

暂存区代码还原并清除暂存区记录：

`git stash pop`

清空所有暂存区的记录：

`git stash clear`

> drop 是只删除一条，当然后面可以跟 stash_id 参数来删除指定的某条记录，不跟参数就是删除最近的，而 clear 是清空。

### merge & rebase

**rebase** 跟 **merge** 都是合并分支，区别是**merge** 暴力合并，能知道代码来自哪个分支;**rebase** 比较合并，按代码的时间来给它重新排序，然后重新放置好，看起来很有逻辑，却不能得知哪个代码来自哪个分支

> note by [bubao](https://github.com/bubao)