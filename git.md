## Git 操作记录 

### 概述
 ```
 # git init     #以建可略
 # git add .  或者  git add *.c  或者 git add app/* //添加要提交的文件
 # git commit -m "desc"     //编辑注释
 # git push origin master   //提交
 # git pull origin master   //更新
    # 切换并新建分支到origin/master , 如果没得 -b 就是光切换
    # git checkout -b origin/master
    # 如果切换不起执行
    # git reset --merge
    # 如何解决failed to push some refs to git
    # git pull --rebase origin master
 # 绑定git地址 //可略
 # git remote add origin https://github.com/xxxsina/zhibo.git
 
 # 删除绑定git地址
 # git remote rm origin
 
 # 当因为远程库与本地库不一致时，那么我们把远程库同步到本地库就可以了
 # git pull --rebase origin master
 
 # 查看当前仓库地址
 # git remote show origin
 ```
 ### 新建分支
 ```
 # git checkout -b iss53    //切换分之到iss53
    # 相当于执行了
    # git branch iss53
    # git checkout iss53
    # git checkout config/  //文件夹或者文件，则返回当前修改，保持跟仓库上的代码一致
 # 分支的提交方式
 # git push origin use_swoole
 # 查看当前分支
 # git branch -al
 # 远程和本地绑定
 # git branch -vv
 ```
 ### 合并分支
 ```
 # 先回到master分支
 # git checkout master
 # 然后执行 git merge 跟上 hotifx分支名
 # git merge hotfix
 ```
 ### 撤销
 ``` 
 # 撤销到之前版本
 # git reset --hard HEAD^
 # 撤销缓冲区（在commit之前）
 # git reset HEAD 111.txt
 # git reset origin/master
 ```
 ### git其他操作
 ``` 
 # git项目中有时候会在本地增加或者删除了一些文件或者文件夹，但是又不想提交，一般情况下，我们取消本地所有修改
 # git checkout .
 # 取消指定文件修改
 # git checkout  filename
 # 取消指定文件删除
 # git checkout  filename
 # 恢复到上一个版本，则可以解决整个文件夹删除的修改
 # git reset --hard HEAD^
 # 取消本地增加的文件和所有修改
 # git checkout . && git clean -df
 ```
### 其他
``` 
# 使用git stash命令保存和恢复进度
# https://blog.csdn.net/daguanjia11/article/details/73810577
# https://www.jianshu.com/p/14afc9916dcb
# git stash
# 说明：保存当前工作进度，会把暂存区和工作区的改动保存起来，执行完这个命令后，在运行git status命令，就会发现当前是一个干净的工作区，没有任何改动。使用git stash save 'message...'可以添加一些注释
# git stash list
# 显示保存进度的列表。也就意味着，git stash命令可以多次执行。
```
``` 
记住密码
	方法一、
	永久记住密码
	git config --global credential.helper store
		会在用户主目录的.gitconfig文件中生成下面的配置。
		[credential]
		    helper = store
	如果没有--global，则在当前项目下的.git/config文件中添加。
	方法二、
	当然，你也可以直接复制上面生成的配置到配置文件中。
	1、在C:\Users\xxx下新建.gitconfig文件
	2、编辑器打开，输入如下内容
	[credential]
		helper = store
	参考资料
	https://blog.csdn.net/flw8840488/article/details/86634244
	https://www.jianshu.com/p/6c539d1956d5
```
``` 
参考资料
https://www.cnblogs.com/lingqiang0605/p/10310350.html
https://www.cnblogs.com/laogui/articles/5897438.html 
```
### 问题处理
```
关于git提示“warning: LF will be replaced by CRLF”终极解答
https://www.jianshu.com/p/450cd21b36a4
解决问题 : 
方法一、
#提交时转换为LF，检出时转换为CRLF
$ git config --global core.autocrlf true
方法二、
#提交时转换为LF，检出时不转换
$ git config --global core.autocrlf input
方法三、
#提交检出均不转换
$ git config --global core.autocrlf false
```