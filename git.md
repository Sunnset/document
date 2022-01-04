[返回](index.md)

# Git操作命令

## Git配置
> Git配置文件优先级：仓库级别(local) > 用户级别(global) > 系统级别(system)。仓库级别对应配置文件是当前仓库下的.git/config， 用户级别对应的配置文件是当前用户目录下的~/.gitconfig，系统级别对应的配置文件是git安装目录下的 /etc/gitconfig。

 - 查看仓库配置：`git config --local -l `
 - 查看用户配置：`git config --global -l `
 - 查看系统配置：`git config --system -l `
 - 查看所有配置：`git config -l `
 - 配置编辑器：`git config --global core.edit emacs`
 - 编辑配置文件：`git config [--local|--system|--global] -e`
 - 添加一个配置项：`git config [--local|--system|--global] --add section.key value`
 - 获取配置项：`git config [--local|--system|--global] --get section.key`
 - 删除配置项：`git config [--local|--system|--global] --unset section.key`
 - 中文乱码处理：`git config --global core.quotepath false`
 - 定义全局的用户名：`git config --global user.name "……"`
 - 定义全局的邮件地址：`git config --global user.email "……"`
 - 配置git客户端保存密码：`git config --global credential.helper store`
 - 不校验https证书：`git config [--local|--system|--global] http.sslVerify "false"`

### 颜色配置
```
[color]
        ui = auto
[color "branch"]
        current = yellow reverse
        local = yellow
        remote = green
[color "status"]
        added = yellow
        changed = green
        untracked = cyan
[color "diff"]
        meta = yellow
        frag = magenta bold
        commit = yellow bold
        old = red bold
        new = green bold
        whitespace = red reverse
[color "diff-highlight"]
        oldNormal = red bold
        oldHighlight = red bold 52
        newNormal = green bold
        newHighlight = green bold 22
```

### 配置提交信息模板

> 该配置经测试仅对图形化工具生效

```
[commit]
        template = /Users/zbwang/.gitcommit_template


.gitcommit_template:
<type>(<scope>)：<subject>

<body>

<footer>
```


## 远程仓库
- 检出仓库：`git clone url localFolderName`
- 查看远程仓库：`git remote -v`
- 添加远程仓库：`git remote add [name] [url]`
- 删除远程仓库：`git remote rm [name]`

## 分支操作
### 查看分支命令
- 查看本地所有分支：`git branch`
- 查看远程所有分支：`git branch -r`
- 查看本地和远程所有分支：`git branch -a`
- 本地切换分支：`git switch branchName`或者`git checkout branchName`
- 本地创建分支：`git branch newBranchName`
- 本地创建分支并且到新建分支：`git checkout -b newBranchName`
- 本地分支删除：`git branch -d branchName`，==警告：删除分支的时候不能在要删除的分支上执行操作==。
- 提交本地分支到远程仓库：`git push origin branchName`
- 删除远程分支：`git push --delete origin branchName`
- 创建没有父分支的分支：`git checkout --orphan newbranchname`

### 分支操作
 - 将本地修改文件添加版本控制：`git add [.|文件路径]`
 - 将本地版本控制下的修改提交到本地：`git commit -m "提交说明"`
 - 将本地修改推送到远程：`git push origin branchname`
 - ：`git getch`
 - ：`git pull`
 - 将branchname合并倒当前分支：`git merge -no-ff branchname`

## 堆栈操作
 - 将所有未提交的修改保存到堆栈中：`git stash`
 - 将所有未提交的修改保存到堆栈中：`git stash save "name"`
 - 查看当前堆栈中的列表：`git stash list`
 - 将堆栈中的内容弹出应用当当前分支并删除内容：`git stash pop`
 - 将堆栈中的内容弹出应用当当前分支不删除内容：`git stash apply [name]`
 - 删除指定名称的堆栈：`git stash drop name`
 - 删除堆栈里的所有内容：`git stash clear`
 - 查看最新保存[指定名称]的与当前目录的差异：`git stash show [name]`，`git stash -p [name]` 可查看详细差异。
 - 从最新的stash创建分支：`git stash branch`，应用场景：当储藏了部分工作，暂时不去理会，继续在当前分支进行开发，后续想将stash中的内容恢复到当前工作目录时，如果是针对同一个文件的修改（即便不是同行数据），那么可能会发生冲突，恢复失败，这里通过创建新的分支来解决。可以用于解决stash中的内容和当前目录的内容发生冲突的情景

## 标签操作
 - 打印所有标签：`git tag`
 - 打印符合检索条件的标签：`git tag -l 1.*.*`
 - 查看对应标签状态：`git checkout 1.0.0`
 - 创建标签：`git tag 1.0.0-light`
 - 创建带备注标签：`git tag -a 1.0.0 -m "这是备注信息"`
 - 针对特定commit版本SHA创建标签：`git tag -a 1.0.0 0c3b62d -m "这是备注信息"`
 - 删除标签(本地)：`git tag -d 1.0.0`
 - 将本地所有标签发布到远程仓库：`git push origin --tags`
 - 指定版本发送：`git push origin 1.0.0`
 - 删除远程仓库对应标签（Git版本 > V1.7.0）：`git push origin --delete 1.0.0`
 - 删除远程仓库对应标签（Git版本 <= V1.7.0）：`git push origin :refs/tags/1.0.0`