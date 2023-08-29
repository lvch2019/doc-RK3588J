# 前言
记录开发遇到的一些问题和解决

# git使用流程
- 将工作区代码做`堆栈`暂存
- git pull 远端代码
- 暂存拉应用后确认是否冲突
- 解决冲突
- git add .
- git commit -m "message"
- git push 

# 一些好用的功能
## git cherry-pick -x HASH
## 多分支

## 回滚相关
```

本地回滚 
g'it reset --hard commit-id
git reset --hard HEAD ~3 最近3次 

远端回滚
git reset --hard commit-id 
git push origin  --force
```

## 分支相关
```
修改分支名更新到origin

本地修改
git branch -m oldbranchname newbranchname
推送
git push origin : oldbranchname 
git push --set-upstream orgin newBranchName


删除本地分支
git branch -d <local_branch>
删除远端的分支
git push origin<remote_name> -d /feature/test1<remote_branch>
或
git pushorigin:分支名


git remote show <remote_name>


本地分支与远程分支关联，并推送到远程仓库
git push --set-upstream origin dev (假设我本地创建了一个名为dev的分支，远程仓库还没有这个分支，推送的命令是：)
如果有
git push origin 分支名
```