# 前言
记录开发遇到的一些问题和解决
***
# git使用流程
- 将工作区代码做`堆栈`暂存
- git pull 远端代码
- 暂存拉应用后确认是否冲突
- 解决冲突
- git add .
- git commit -m "message"
- git push 
***
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
***
## 如果优雅的使用git