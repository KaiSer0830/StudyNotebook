### Git操作指令

##### 注册信息

```
username	KaiSer0830
```



##### 初始化Git仓库

```
git init  
```



##### 设置git用户名／邮箱

```
git config --global user.name 'github用户名'
git config --global user.email '邮箱'
```



##### 关联远程仓库

```
git remote add origin https://github.com/CongliYin/CSS.git
```



##### 查看配置(包含：用户名和邮箱等)

```
git config --list
```



##### 初始化一个新的Git仓库

```
创建文件夹	mkdir 文件名
进入文件夹	cd	文件名
在文件夹内初始化git，生成.git文件	git init
```



##### 在文件夹内生成文件

```
touch 文件
或者 vim 文件
```



##### 上传文件到仓库

```
查看当前状态	git status
上传某文件到暂存区	git add 文件名	
上传全部文件到暂存区	git add *	或者 git add .
提交上传文件的信息	git commit -m '提交信息' 
同步到远程仓库	git push origin master

如果出现错误：
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
则先进行 git pull 操作，再执行 git push 操作
或者git push -f 
可以提交，会将remote上第一个人的改动冲掉，比较暴力，不太好。

如果出现错误：
fatal: The remote end hung up unexpectedly
修改提交缓存大小为500M，或者更大的数字
git config --global http.postBuffer 524288000
git config --global http.postBuffer 1048576000
或者在克隆/创建版本库生成的 .git目录下面修改生成的config文件增加如下：
[http]  
postBuffer = 524288000
配置git的最低速度和最低速度时间：
git config --global http.lowSpeedLimit 0
git config --global http.lowSpeedTime 999999


如果出现错误：
error: RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054
使用	git config http.sslVerify "false"
```



##### 更新仓库文件

```
查看修改的内容		git status
上传所有修改内容	git add -A
提交上传文件的信息	git commit -m '提交信息' 
如果使用 git push 出错，则使用 git push origin master -f
```



##### 删除仓库文件

```
删除文件	git rm -rf 文件名
从Git中删除文件	git rm 文件名
提交操作	git commit -m '提交信息' 
```



##### 下载仓库文件

```
git clone 地址
```



##### 当无法同步，没有权限时

```
The requested URL returned error:403 Foridden while accessing
```

```
答案：私有项目，没有权限，输入用户名密码，或者远程地址采用这种类型

vi .git/config

#将
[remote "origin"]
	url = https://github.com/用户名/仓库名.git
修改为：
[remote "origin"]
	url = https://用户名：密码@github.com/用户名/仓库名.git
```



##### 分支

```
创建分支（注意创建后并不会自动切换到此分支）	git branch 分支名
切换到此分支	git checkout 分支名
新建并切换一个分支	git checkout -b 分支名
合并分支	git checkout master		git merge 分支名
删除分支	git branch -d 分支名


```



##### git拉取远程分支到本地

```
初始化		git init
与origin master建立连接	git remote add origin git@github.com:XXXX/nothing2.git
把远程分支拉到本地	git fetch origin dev（dev为远程仓库的分支名）
本地创建分支dev并切换到该分支	git checkout -b dev(本地分支名称) origin/dev(远程分支名称)
把某个分支上的内容都拉取到本地		git pull origin dev(远程分支名称)
```



##### refusing to merge unrelated histories

```
git pull --allow-unrelated-histories
```





