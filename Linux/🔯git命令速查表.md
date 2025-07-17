# Git命令速查表

|命令|说明|
| ------| ---------------------|
|​`git clone <url>`​|克隆远程仓库|
|​`git init`​|初始化本地 Git 仓库|

## 本地更改

|命令|说明|
| ------| --------------------------------------|
|​`git status`​|查看当前分支状态|
|​`git diff`​|查看已跟踪文件的变更|
|​`git add <file>`​|将指定的文件添加到暂存区|
|​`git add .`​|将所有有变更的文件添加到暂存区|
|​`git commit -m "xxx"`​|提交已添加至暂存区的文件，并添加描述|
|​`git commit -am "xxx"`​|添加并提交所有修改|
|​`git commit --amend -m "xxx"`​|修改上一次提交（谨慎使用）|
|​`git stash`​|暂存当前修改，将所有置为 HEAD 状态|
|​`git stash list`​|查看所有暂存列表|
|​`git stash push`​|将当前工作区文件暂存到临时空间|
|​`git stash pop`​|从临时空间恢复文件到当前工作区|

## 提交历史

|命令|说明|
| ------| ----------------------------------|
|​`git log`​|查看提交日志|
|​`git log -n`​|显示 n 行日志|
|​`git log --stat`​|查看本地提交日志|
|​`git show <commit>`​|查看指定提交的日志及相关变动文件|
|​`git show HEAD`​|查看 HEAD 提交日志|
|​`git show HEAD^`​|查看 HEAD 的上一个版本提交日志|
|​`git blame <file>`​|逐行显示文件的提交信息|
|​`git whatchanged`​|显示提交历史及变更文件|

## 分支和标签

|命令|说明|
| ------| ----------------------------|
|​`git branch`​|查看本地分支|
|​`git branch -r`​|查看远程分支|
|​`git branch -a`​|查看所有分支（本地和远程）|
|​`git branch --merged`​|查看已合并到当前分支的分支|
|​`git branch --no-merged`​|查看未合并到当前分支的分支|
|​`git branch <new-branch>`​|创建新分支|
|​`git checkout <branch-name>`​|切换到指定分支|
|​`git branch -d <branch-name>`​|删除本地分支|
|​`git tag`​|列出所有本地标签|
|​`git tag <tag-name>`​|基于最新提交创建标签|
|​`git tag -d <tag-name>`​|删除标签|

## 删除命令

|命令|说明|
| ------| ----------------------------|
|​`git rm <file>`​|删除文件（从磁盘中删除）|
|​`git rm -r <directory>`​|递归删除指定目录下的文件|
|​`git rm --cached <file>`​|停止跟踪文件，不从磁盘删除|

## 合并和衍合

|命令|说明|
| ------| --------------------------------------|
|​`git merge <branch>`​|合并指定分支到当前分支，保留两个分支|
|​`git rebase <branch>`​|合并指定分支到当前分支，只保留一个|
|​`git rebase --abort`​|终止 rebase 操作|
|​`git rebase --continue`​|解决冲突后继续 rebase|
|​`git mergetool`​|使用配置文件指定的合并工具解决冲突|

## 撤销命令

|命令|说明|
| ------| ------------------------------------|
|​`git reset --hard HEAD`​|将当前版本重置为 HEAD|
|​`git reset <commit>`​|重置为某个提交状态，代码不变|
|​`git reset --hard <commit>`​|强制重置为某个提交状态（谨慎使用）|
|​`git revert <commit>`​|撤销提交|
|​`git restore <file>`​|丢弃文件修改，恢复到修改前状态|
|​`git clean`​|清除未跟踪的文件|
|​`git clean -n`​|列出将被删除的未跟踪文件|

## 配置命令

|命令|说明|
| ------| ---------------------------|
|​`git config --list`​|列出当前 Git 配置|
|​`git config --global user.name <name>`​|设置提交者姓名|
|​`git config --global user.email <email>`​|设置提交者邮箱|
|​`git config --global alias.<alias> <command>`​|为 Git 命令创建全局别名|
|​`git config --global color.ui auto`​|使用颜色渲染 Git 命令输出|

## 其他命令

|命令|说明|
| ------| --------------------|
|​`git var -l`​|列出 Git 环境变量|
|​`git help <command>`​|显示指定命令的帮助|

**注意事项：**

* 某些命令可能会导致数据丢失，请谨慎使用
* 建议在执行重要操作前备份代码

‍
