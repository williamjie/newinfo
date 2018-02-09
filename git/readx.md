

git remote show origin

git remote remove origin




git remote -v 查看现有远程仓库的地址url



三种方式都可以。

1. 修改命令
git remote set-url origin <URL> 更换远程仓库地址。把<URL>更换为新的url地址。

2.先删后加
git remote rm origin 
git remote add origin git@github.com:Liutos/foobar.git 

3. 直接修改config文件



但是你可能想要把你的本地的git库，既push到github上，又push到开源中国的Git@OSC上，怎么解决呢。
有人可能会用两个甚至多个远程库，即再添加一个远程库git remote add origin2; 
这个方法很低效，因为你要git push 两次才能完成push到两个库。

其实还有一个方法，git的一个远程库 可以对应多个地址，即我能让 远程库origin拥有多个url地址。 
方法如下：

使用流程

首先，我们从零开始， 
假设你现在想要增加3个远程库地址，分别为 :

https://git.oschina.net/shede333/swioslibary.git 
https://git.oschina.net/shede333/swscrollbar.git 
https://github.com/shede333/CoreAnimationTestSW.git

首先，先增加第一个地址 git remote add origin <url1> 
然后增加第二个地址 git remote set-url --add origin <url2> 
增加第三个地址 git remote set-url --add origin <url3> 
….依次类推

这样就完成了添加多个地址到origin库中了， 
以后只要使用git push origin master 就可以一次性push到3各库里面了(使用git push也可)

原理解析

git remote set-url --add origin 就是往当前git项目的config文件里增加一行记录 
config文件打开方式有两种：

使用命令git config -e
在当前git项目的根目录下，文件位于 .git/config (.git目录为隐藏文件)
你每执行一次git remote set-url --add origin 就会增加一行，如下图：

git remote -v:显示当前所有远程库的详细信息，显示格式为 远程库名字 url连接(类型)

git-remote

所以说，你直接在config里面直接添加url来修改也是可以的，不必去执行git命令。

注意

使用git push origin master时，你可以push到origin的多个url地址， 
但是使用 git pull时，只能拉取origin里的一个url地址(即fetch-url，如上图)，这个fetch-url默认为 你添加的到origin的第一个地址， 
如果你想更改，只需要更改config文件里，那三个url的顺序即可，fetch-url会直接对应排行第一的那个utl连接。




