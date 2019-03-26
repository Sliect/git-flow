# git-flow

> 开发阶段: 在develop分支上拉出feature分支进行开发
>
> 联调阶段/测试阶段: 新建联调分支release并合并feature分支进行联调、测试
>
> 发布阶段: 将release分支合并到master分支 进行发布

## 初始化
> git branch develop
>
> git push -u origin develop 默认选择develop分支推送

## 新增功能
> git checkout -b some-feature develop 基于develop分支创建some-feature分支
>
> git checkout some-feature 切换到some-feature分支

## 联调分支
> git checkout -b release-0.1 新建并切换到release-0.1分支
>
> git merge some-feature
>
> git merge other-feature
>
> 反馈问题 => 在各自功能分支上进行修改 => 合并功能分支直至没有问题

## 将联调完成的分支合并到develop分支
> git pull origin develop 拉取develop分支
>
> git checkout develop 切换开发分支
>
> git merge release-0.1 合并分支
>
> git push 推送分支
>
> git branch -d some-feature 删除功能分支
>
> git branch -d other-feature

## 发布版本
> git checkout master
>
> git merge release-0.1
>
> git push
>
> git branch -d release-0.1
>
> git tag -a v-0.1 -m "Initial public release" master
>
> git push --tags

## 修复Bug
> git checkout -b issue-#001 master
>
> git checkout master
>
> git status
>
> git add
>
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

## reset回滚代码
> git checkout develop
>
> git log
>
> git reset --hard 36da39b

## revert回滚代码
> git revert HEAD

## 代码处于冲突状态
> 解决冲突后
>
> git add
>
> git commit
>
> git merge --abort 撤销merge

## 突发事件处理
> git add .
> git stash
>
> 切换分支救火后切回原来的分支
>
> git stash pop

## 查看HEAD移动历史
> git reflog 查看所有HEAD移动历史
>
> git reflog master 查看master分支的HEAD移动历史

## rebase对历史操作的修改
> git checkout feature
>
> git rebase master 找到master和feature的最近共同祖先，然后对比当前分支相对于该祖先的历次提交，提取相应的修改并存为临时文件，以master为基，将临时文件的修改依次应用
>
> git checkout master
>
> git merge feature 快进合并，将HEAD指向rebase之后的最新节点

> 上述操作可以简化为
>
> git rebase master feature
>
> git checkout master
>
> git merge feature

> 注意：rebase不能在公共分支上进行操作，但是可以在私有分支上rebase公共分支，e.g: git rebase master

## 丢弃或修改不是最新的提交
> git rebase -i HEAD^^ 进入编辑页面，将至上而下展示从旧到新的提交节点，将pick改为edit可以修改之前的提交内容，将pick这行删除可以撤销这次提交

> git rebase --onto [目标] [起点] [终点] 找到目标和终点的最近共同祖先，不包含起点的提交节点，然后将这些节点保存为临时文件，以目标为基，将临时文件的修改依次应用
>
> git checkout [目标]
>
> git merge [终点] 快进合并