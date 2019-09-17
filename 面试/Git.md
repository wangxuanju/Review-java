# Git
Git是当下最流行、最好用的版本控制系统，比SVN强大的地方就在于其分支管理功能。

mkdir test 创建文件夹test 
cd test切换到test目录
touch a.md新建a.md文件
git status新建状态
git init 初始化git仓库

git add 把改动添加到一个暂存区
git commit真正的提交
git add a.md文件到git仓库，未提交
git rm --Cached移除这个缓存
git commit -m 'first commit'第一次提交

git log查看所有的commit记录
git branch查看当前分支情况
git banch a 新建一个叫a的分支
git checkout a 从master分支切换到a分支
git merge a 把a分支的代码合并到主分支


git branch -d a 把a分支删除了
git branch -D a 把a分支强制删除
git tag 查看历史tag记录

提交代码第一次设置自己的用户名和密码
git config --global user.name "wang"
git config --global user.email "wang@qq.com"
# 起别名
git config --global alias.co checkout
git config --global alias.psm 'push orign master'
git log查看日志

# 
git config --global core.editor "Vim"将编辑由默认vi改为vim
git config --global color.ui true 开启给git着色

git diff 当前文件与暂存区的差异
git diff --staged暂存区与版本库的差异
git diff <# id1> <$id2>两次提交之间的差异
git diff <branch1 >..<branch2>两个分支之间的比较

git checkout v1.0切换到某版本
git checkout ff..ff切换到某次commit

# 放心手中的代码处理另一问题，处理完回来
git stach 当前分支没有commit的代码先暂存
git stach apply之前代码代码又从新回来了
git stach drop 把这次的stach记录删除
git stach pop （pop与apply的区别，pop不但会把代码还原而且还把stach记录删除）
git stach clear 清除所有暂存区记录


# 分支管理
git branch develop 新建develop分支
git checkout develop 切换到develop分支

git push orign develop 把develop分支推送到远程仓库
git push orign develop：develop2 远程仓库取名develop2（一般本地与远程仓库命名一致）


分支管理工具Git Flow
master即将发布--hotfix修复master上的问题---release准备发布版本的分支--develop最新发布状态--feature开发新功能分支

git branch feature/A 做一个新功能A
git branch hofix/B 线上bug修复
git branch release/1.0感觉可发布到正式环境了


