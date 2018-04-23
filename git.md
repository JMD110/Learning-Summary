#### git常用命令:
|    命令          |    说明                      |
| :---------------: | :--------------------------: |
|git clone '远端克隆地址'| 将仓库克隆并创建链接到本地|
|git checkout -b '分支名'| 创建并进入分支         |
|git checkout '分支名'  | 进入分支                |
|git status            | 查看修改文件状态         |
|git add '文件名'       | 添加要上传的文件|
|git add .             | 添加所有文件       |
|git commit -m '说明'   | 提交并添加文件说明|
|git push origin '分支名'| 提交文件到远端的分支中|
|git pull origin '分支名'|如果远端修改了文件二本地并未更新,需pull从远端先把本地更新了才能push到远端分支|
|git merge '分支名'  | 将你当前所在分支与'分支名'分支进行融合|
|git stash           |缓存更改                        |
|git stash list      |查看缓存片段                     |
|git stash apply stash@{0}| 还原缓存代码|
|git log             |查看提交的日志         |
|git -a '版本号' -m '说明'|提交上线版本标签及说明|
|git push origin '标签名'| 将上线版本push到远端|
|git show commit-id| 查看某次提交的内容|
|git reset --hard  |退回到以前的版本|
|git branch -D '分支名'|删除该分支|
|git push origin --delete '分支名'|删除远端分支|
|git push origin --delete tag '版本号'|删除远端上线版本|
|git diff '分支名' '分支名'| 看两个分支间的差异|