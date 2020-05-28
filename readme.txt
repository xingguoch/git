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
git checkout -- "要撤销文件名"  
撤销工作区修改的内容，一种是：修改了工作区内容还没有添加到暂存区；
		  第二种是：添加到暂存区后，修改了工作区的内容；

git reset HEAD "要撤销的文件名" 可以撤销添加到暂存区的内容

删除文件：
rm "工作区文件"  删除工作区文件
git rm “版本库文件” 删除版本库文件
git checkout -- “把删除的工作区文件还原到最新版本”

远程仓库（github）
本地git仓库和github仓库之间传输需要通过SSH加密的，需要设置一下步骤：
1、创建SSH Key。ssh-keygen -t rsa -C “邮箱”回车；
     在用户主目录下可以找到.ssh目录，里面又两个文件夹：id_rsa(私钥，不能泄漏出去) 和 id_rsa.pub (公钥，可以放心给别人);
2、登录github，打开account settings，然后点击 SSH and GPG keys 添加公钥；可添加多个Key，github是免费托管git仓库
    任何人都可以看到（但只有自己可以修改），不能放入敏感信息
    如果不想让别人看到你的内容可以设置私有仓库、或是搭建私有github服务器

添加远程仓库






 
