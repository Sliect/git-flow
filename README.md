# git-flow

## 初始化
> git branch develop
>
> git push -u origin develop 默认选择develop分支推送

## 新增功能并添加到主干
> git checkout -b some-feature develop 基于develop分支创建some-feature分支
>
> git checkout some-feature 切换到some-feature分支
>
> git status
> git add
> git commit
>
> git pull origin develop 拉取develop分支
>
> git checkout develop 切换开发分支
>
> git merge some-feature 合并分支
>
> git push 推送分支
>
> git branch -d some-feature 删除功能分支

## 修复Bug
> git checkout -b issue-#001 master
>
> git checkout master
>
> git status
> git add
> git commit
>
> git checkout master
>
> git merge issue-#001
>
> git push

## 在develop分支中添加 issue-#001 的补丁
> git checkout develop
>
> git merge issue-#001
>
> git push
>
> git branch -d issue-#001