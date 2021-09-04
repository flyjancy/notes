# Git常用命令总结

## 基础流程

创建git仓库

`git init`

克隆一个仓库

`git clone <path>`

添加改动到stage

`git add *`

提交改动到HEAD

`git commit -m "commit message"`

将改动推送到远端仓库的main分支，main可以替换为其他分支名称

`git push origin main`

更新本地仓库至最新改动

`git pull`

## 版本控制

获取提交ID

`git log`

给提交ID创建标签(example id: 1b2e1d63ff)

`git tag 1.0 1b2e1d63ff`

查看命令历史

`git reflog`

回退到最新的改动

`git reset --hard HEAD`

回退到最新改动的上一次改动

`git reset --hard HEAD^`

回退到某一次改动

`git reset --hard <commit_id>`

## 分支开发

创建分支

`git branch <branch_name>`

查看当前分支

`git branch`

切换到某一个分支

`git switch -c <branch_name>`

合并某分支到当前分支

`git merge <branch_name>`

删除分支

`git branch -d <branch_name>`