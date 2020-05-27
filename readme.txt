git 分布式版本控制系统。
git init 初始化
git add 将代码存储在暂存区（stage）
git commit -m “备注” 将暂存区的数据推到远程服务器上
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
 
