之前用过git一段时间，在一位学长的带领下用git团队开发协作了一个vue的小程序，在很长一段时间里面就没有用过git了，近段时间研究了一下springboot，写了个小demo，把他上传到github上，突然发现，自己对git的命令完全忘了。。。。。下面把这些命令记在博客上，以防再次遗忘。

1.git init

### 初始化本地仓库

2.git remote add origin 你的仓库地址 （git remote remove origin）

### 关联本地仓库到远程仓库

3. git add *

### 添加要提交的文件到暂存区

4.git commit -m "init commint"

### 提交代码到文件控制仓库

5.git fetch origin

### 将远程主机的更新，全部取回本地

6.git pull origin master    如果报错用这个 git pull origin master --allow-unrelated-histories

### 拉取远程分支代码到本地

7.git push -u origin master:master

### 提交本地分支(master)代码到远程分支(master)
<<<<<<< HEAD


- [x] 如果远程是空仓库,在 commit 后可以使用 git push -u origin "master" ✅ 2024-02-24

=======
>>>>>>> origin/master

### 克隆指定分支
![image.png](https://iili.io/JGotIbj.png)

### 切换分支
![image.png](https://iili.io/JGot05g.png)
