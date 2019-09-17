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











