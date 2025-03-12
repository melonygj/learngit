## 1.创建一个新的仓库
初始化一个Git仓库，使用`git init`命令
添加文件到Git仓库，分两步:
1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m <message>`，完成。
3. 要随时掌握工作区的状态，使用`git status`命令。
4. 如果`git status`告诉你有文件被修改过，用git diff 可以查看修改内容
## 2.版本回退
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令 `git reset --hard commit_id`。  
穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。  
要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
## 3.撤销修改
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区,想丢弃修改时，用命令`git reset HEAD file`。
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
## 4.删除文件
场景1：从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`
场景2：如果删错了使用 `git checkout -- file` 可以把文件恢复到最近一次`git commit`或`git add`时的状态。
## 5.添加远程库
想要关联一个远程库，使用命令`git remote add origin git@github.com:melonygj/learngit.git`   
关联一个远程库的时候必须给远程库指定一个名字`orgin` 是默认习惯命名。   
关联后，使用命令`git push -u origin master` 第一次推送master分支的所有内容。  
此后每次本地提交后，只要有必要就可以使用`git push origin master` 推送最新修改。
## 6.从远程库克隆
使用git clone命令克隆，Git支持多种协议包括https,但ssh协议速度最快。

## 7. 创建并合并分支
创建分支,并切换到该分支：`git checkout -b dev`  
它相当于一下两条命令：
`git branch dev`  `git checkout dev`  
使用`git branch` 命令查看当前分支
合并分支 `git merge dev`，将指定分支（dev）合并到当前分支。  
合并完成之后，可以放心删除dev分支，`git branch -d dev`。
创建并切换到新的dev分支，也可以使用：
`git switch -c dev`
直接切换到已经有的master 分支，可以使用
`git switch master`  
用`git log --graph` 命令可以看到分支合并图
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合
## 8. bug分支
修复bug时，我们会通过创建新的bug分支进行修复然后合并，最后删除；
当手头工作没有完成时，先把工作现场 `git stash`一下，然后去修复bug，修复后再 `git stash pop`回原工作现场。    
在 master分支上修复的bug，要合并到dev分支上，就需要 `git cherry-pick <commit>` 命令,把bug提交的修改复制到当前分支，便面重复劳动。
如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`



