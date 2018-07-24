
# git基本操作语法
### 本地配置
```
    配置用户信息
    git config --global user.name 'yo ti' //设置用户名，必须使用注册github的名称
    git config --global user.email 'git_yoti@tutanota.com' //设置邮箱，
    git config --global credential.helper cache // 设置密码缓存15分钟不用输入密码
    配置ssh
    cat ~/.ssh/id_rsa.pub //读取密钥(公共密钥)
    ssh-keygen -t rsa -C 'git_yoti@tutanota.com' //私有密钥
    ssh -T git@github.com //测试是否链接正常
    到github网站将ssh 参数进行设置即可进行提交托管操作。 
```


###`基础语法`

|语法|描述|其他|
|---|---|---|
|`git clone+仓库地址`|克隆仓库到本地|1|
|`git add 文件`|将文件提交到暂存区|保存为草稿|
|`git commit -m '提交描述'`|提交到提交区|1|
|`git status`|查看修改状态|-|
|`git checkout -- 文件`|放弃该文件的修改内容|必须最少一次`add`或`commit`|
|`git rm 文件`|删除本地文件|0|
---
###`提交到远程`+`分支相关`

|语法|描述|其他|
|---|---|---|
|`git push`|将文件提交到远程区域|-|
|`git push --set-upstream origin 分支名`|创建远程分支|-|
|`git push -u origin _gulp:_gulp`|将本地的分支创建到远程|-|
|`git branch`|0|查询本地的分支列表|
|`git branch 分支名称`|0|创建本地分支并切换|
|`git checkout -b 分支`|0|同上创建本地分支并切换|
|`git checkout 分支名称`|0|切换到分支,分支部分文件也会消失|
|`git branch -r`|0|查看远程分支列表|
|`git branch -a`|0|查看远程+本地分支列表|
|`git branch -d 分支名称`|0|删除分支|
|`git branch -D 分支名称`|0|强制删除分支|
|`git branch -d -r 分支名称`|0|删除远程端分支|
|`git merge --on-ff 分支`|分支合并|0|
---
###`日志相关`

|语法|描述|其他|
|---|---|---|
|`git log`|查看日志|哈希值+作者+日期+提交描述|
|`git log --pretty=short`|0|哈希值+作者+提交描述|
|`git log -p`|0|哈希值+作者+日期+提交描述+增删的细节|
|`git log --graph`|0|哈希值+作者+日期+分支合并细节|
|`git log 文件名`|0|指定文件的数据|
|`git diff`|0|用于查看那些文件发生了修改|
|`git status`|0|查看项目状态|
---
###`回滚操作`

|语法|描述|其他|
|---|---|---|

|`git reset HEAD file`|||
|`git reset 哈希值`|回滚状态到对应哈希值位置|前提在为提交到远程,否则会冲突|


### `其他`

|语法|描述|其他|
|---|---|---|
|`git commit --amend -m '修改提交信息'`|修改提交仓库的描述|未测试|
|`git pull`|将文件更新到最新|未测试|
|`git remote add origin git@github.com:gityoti/_gulp.git`|未知|未测试|
|`git tag 0.1.0`|0|版本管理|
|`git push origin --tags`|0|版本提交到远程|
|``|||
|``|||

### `linux指令`
|语法|描述|其他|
|---|---|---|
|`touch aaa.txt`|目录下创建文件|0|
|`mkdir aaa`|创建文件夹|0|
|`vim aaa.txt`|编辑文件内容|不好用|
|`cd 文件夹`|切换到文件夹||
|`cd..`|回退到上级目录||
|`cat aaa.txt`|查看文件内容||
|`rm xxx`|删除本地文件||
|``|||


### `报错解决`
    #1 fatal: unable to access 'https://github.com/gityoti/git_test.git/': Failed to connect to 127.0.0.1 port 8580: Connection refused
    		1） git push 时候出现的,git clone 时候出现
    		[解决] 挂上代理就可以了? 这是怎么回事??
    	#3 To https://github.com/gityoti/git_test.git
     	 ! [rejected]        master -> master (non-fast-forward)
    	 error: failed to push some refs to 'https://github.com/gityoti/git_test.git'
    	 hint: Updates were rejected because the tip of your current branch is behind
    	 hint: its remote counterpart. Integrate the remote changes (e.g.
    	 hint: 'git pull ...') before pushing again.
    	 hint: See the 'Note about fast-forwards' in 'git push --help' for details.
    		1) git push 时候出现 ##
    		** 翻译 提示：由于当前分支的尖端位于后面，因此更新被拒绝
    		** 不知道是什么原因造成的?? ## 版本修改轨迹跟踪不到了??
    			库[a版本，b版本，c版本] => 将c版本进行上传~ ==> 本地库回退到 b版本 !~ ==> 基于b版本的修改企图覆盖c版本 ==> 然后就版本冲突了
    	[ 解决 ]
    		#方法1:[ git push -u origin master -f ] 强制push ( ok )（ 有缺点~ ）
    		#方法2:[ git pull origin master ][ git push -u origin master ] //# 将远程的pull 下来
    		#方法3:[ git branch branchname ][ push ][ git push -u origin [name] ] //# 通过分支进行push???

    提问
    	#1 ## 选择一个比上传版本低的文件进行修改 ==> 进行上传~ 会出现什么问题?
    		## 会出现版本冲突 ## 需要进行强制push.

    	//# 版本回溯 ## 为什么还原失败??? ## 怎么进行还原???  ## git log 查看版本哈希值!!
    		git reset --hard 8384f2f96a04ea914ab22b60408cc7ef68aab573
    		git checkout 8384f2f96a04ea914ab22b60408cc7ef68aab573