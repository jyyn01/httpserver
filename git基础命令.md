## git基础命令

git init

git init 《目录》 //在这个目录下创建仓库

git status  //显示仓库状态

ls -a //查看隐藏的目录，工作区

git ls-files //查看暂存区内容

git add //添加到暂存区

git commit  [-m] "携带信息"//添加到本地仓库

git commit -am "携带信息" 同时完成add和commit命令

git log [--oneline] //查看提交记录

git reset --soft 回退的版本id //回退版本保留工作区和暂存区

git reset --hard 回退的版本id//都不保存

git reset --mixed 回退的版本id//默认，保留工作区，丢弃暂存区

git diff 默认查看工作区和暂存区的差异

git diff 查看两个分支的区别

git diff HEAD 比较工作区和仓库区别

git diff --cached 比较暂存区和仓库

git diff HEAD~ HEAD 比较最新版本和倒数第二版本区别

git diff HEAD~3 HEAD file3.txt 比较最新版本和倒数第4版本的file3.txt的差别

git rm file 把文件从工作区和暂存区一起删除

git rm --cached file 只删除暂存区  后面都需要commit同步仓库

git remote add origin（别名） url 关联本地仓库和远程仓库

git remote -v 查看当前仓库所对应的远程仓库的别名和地址

git push -u <远程仓库名><分支名>

git pull <远程仓库名><远程分支名>:<本地分支名> 如果相同可以省略冒号后面的部分

git branch 查看仓库的所有分支

git branch 分支名 创建一个新的分支

git checkout 分支名 恢复文件 （切换到其他分支）不常用

git switch 分支名 切换分支

git merge dev 在main分支里合并dev分支

git branch -d dev 删除已经合并的dev分支

git branch -D dev 删除还没有合并的dev分支

