git 分布式版本控制系统。工作区和暂存区
git init 初始化
git add “文件名”“文件名” 将文件修改添加到暂存区（stage）；
git commit -m “备注” 提交更改，将暂存区的所有内容提交到当前分支，git会自动为我们创建唯一一个
	master分支，所以git commit就往master分支上提交更改；
	简单可以理解：需要提交的文件修改统统放在暂存区，然后一次性提交暂存区的所有修改内容；
	
git status 可以掌握工作区的状态
git  diff 如果git status 告诉你修改过文件，可以使用git diff查看修改内容
git log 查看从最近到最远的提交日志，以便确定退回到哪个版本
git reflog 要返回未来，使用该指令查看命令历史，以便确定返回哪个版本
git reset --hard HEAD^ 退回到上一个版本 ；上上一个版本 HEAD^^
	（HEAD指向当前的版本，因此，git允许在版本的历史之间穿梭）
git reset --hard 版本id 返回到最新版本
	（git的版本回退速度快，是因为git在内部有个指向当前版本的HEAD指针，
	当回退版本时，git仅仅时把HEAD指向退回的版本）
cat “文件名” 查看文件内容

管理修改：
如果没有git add到暂存区，就不会加入到commit中

撤销修改：
git checkout -- "要撤销的文件名"  
撤销工作区修改的内容，第一种是：修改了工作区内容还没有添加到暂存区；
		  第二种是：添加到暂存区后，修改了工作区的内容；

git reset HEAD "要撤销的文件名" 可以撤销添加到暂存区的内容

删除文件：
rm "工作区文件"  删除工作区文件
git rm “版本库文件” 删除版本库文件
git checkout -- “把删除的工作区文件还原到最新版本”，其实是用版本库里的版本代替工作区的版本，
无论工作区是修改还是删除，都可以“一键还原”

远程仓库（github）
本地git仓库和github仓库之间传输需要通过SSH加密的，需要设置一下步骤：
1、创建SSH Key。ssh-keygen -t rsa -C “邮箱”回车；
     在用户主目录下可以找到.ssh目录，里面又两个文件夹：id_rsa(私钥，不能泄漏出去) 和 id_rsa.pub (公钥，可以放心给别人);
2、登录github，打开account settings，然后点击 SSH and GPG keys 添加公钥；可添加多个Key，github是免费托管git仓库
    任何人都可以看到（但只有自己可以修改），不能放入敏感信息
    如果不想让别人看到你的内容可以设置私有仓库、或是搭建私有github服务器

添加远程仓库
1、git remote add origin git@github.cm:用户名/仓库名.git  在github仓库创建一仓库，并与本地仓库连接
2、git push -u origin master 将本地仓库内容推送到远程，实际上就是把当前的master主分支推送到远程
     因为远程仓库时空的，我们第一次推送master分支时，加上-u参数，这样本地的master分支与远程的master关联玩起来，
     现在如果要本地提交的话，使用 git push origin master 就可以了。

从远程库克隆
git clone “仓库地址”
git支持多个协议。https 、ssh，ssh要比https协议速度快

创建与合并分支
master分支时一条线，git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点
（HEAD指向当前的分支）

创建分支：git checkout -b dev 等同于 git branch dev 与 git checkout dev

合并分支：合并dev分支就是将master指向dev当前的提交，完成合并
合并分支到master，切回master分支，执行命令：git merge --no-ff -m "合并dev" dev

解决冲突：
我们可以通过git status查看冲突的文件，进入文件查看 :
<<<<<< HEAD
分支上的代码
========
提交的代码
>>>>>>>> 提交分支

分支管理策略：
在Fast forward 模式下，删除分支后，会丢失分支信息
通常合并分支时，我们可以禁用Fast forward模式，并添加commit标记，这样可以从分支历史上看出分支信息
命令行： git merge --no-ff -m "commit标记" dev(分支)

分支策略：
master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活。所以我们都在dev分支上开发，
并将代码跟新到dev上

bug分支：
当我们遇到bug时，我们可以通过创建一个新的临时分支修补bug，修复后，合并分支，然后删除临时分支。
当发现master分支上有bug，但dev上工作正在进行还没有提交：
1、git status 查看工作状态，发现工作进行到一半，还不能提交。
2、git stash 可以把当前的工作储藏起来。等bug修复完成后再继续未完成工作
3、git checkout master 切换到master分支
4、git checkout -b “临时分支” 创建临时分支，在临时分支上进行bug修复，并切回master合并到master；
5、切回dev上，找回之前dev分支上内容：git stash pop 或是多次使用：git stash list ---->git stash apply stash@{0} 
6、dev分支上也需要bug修复，切到dev分支，执行命令：git cherry-pick "临时分支码(ab43722) "，就不用手动修复dev分支bug
 

feature分支：
1、如果需要添加一个新功能，我们可以创建一个新分支，在新分支上开发，完成后，合并，最后删除新分支
2、如果想要丢弃没有合并的分支，可以通过git branch -D <新分支> 强行删除
















