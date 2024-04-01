之前用过git一段时间，在一位学长的带领下用git团队开发协作了一个vue的小程序，在很长一段时间里面就没有用过git了，近段时间研究了一下springboot，写了个小demo，把他上传到github上，突然发现，自己对git的命令完全忘了。。。。。下面把这些命令记在博客上，以防再次遗忘。

```
git init
```
### 初始化本地仓库
```
git remote add origin '你的仓库地址' (git remote remove origin)
```
### 关联本地仓库到远程仓库
```
git add *
```
### 添加要提交的文件到暂存区
```
git commit -m "init commint"
```
### 提交代码到文件控制仓库
```
git fetch origin
```
### 将远程主机的更新，全部取回本地
```
git pull origin master    如果报错用这个 git pull origin master --allow-unrelated-histories
# 如果远程仓库不为空
git pull origin master --rebase

```
### 拉取远程分支代码到本地
```
git push -u origin master:master
```
### 提交本地分支(master)代码到远程分支(master)
- 如果远程是空仓库,在 commit 后可以使用 
```
git push -u origin "master"
```
### 克隆指定分支
![image.png](https://iili.io/JGotIbj.png)

### 切换分支
![image.png](https://iili.io/JGot05g.png)
#### 切换分支后 merge
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240313082638.png)
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240313082709.png)


### git reset 回滚
[git reset基本操作](https://www.jianshu.com/p/cbd5cd504f14)

Git reset 命令有三个主要选项：git reset --soft; git reset --mixed; git reset --hard;

```
git reset --soft
```

将HEAD引用指向给定提交。索引（暂存区）和工作目录的内容是不变的，在三个命令中对现有版本库状态改动最小。

```
git reset --mixed（git reset 默认的模式）
```

HEAD引用指向给定提交，并且索引（暂存区）内容也跟着改变，工作目录内容不变。这个命令会将索引（暂存区）变成你刚刚暂存该提交全部变化时的状态，会显示工作目录中有什么修改。

```
git reset --hard
```

HEAD引用指向给定提交，索引（暂存区）内容和工作目录内容都会变给定提交时的状态。也就是在给定提交后所修改的内容都会丢失(新文件会被删除，不在工作目录中的文件恢复，未清除回收站的前提)。

用表格看起来会更清楚些：

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094023.png)
操作一下看一下实际效果：

首先在一个版本库中修改追踪文件，然后提交，description叫做 **add button**

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094159.png)

使用git log 查看历史提交
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094208.png)

copy记录**add button** 的前一次提交 **add label** 的哈希ID “7c5a658fbceb904ad877c4254d183e68aed1ddd0”，作为我们reset的给定提交。

git stauts 查看一下当前版本库中文件状态
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094224.png)

显示nothing to commit ，在add button 提交后未对版本库中文件做修改

执行**git reset --soft 7c5a658fbceb904ad877c4254d183e68aed1ddd0** 命令，然后使用git status 查看文件状态。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094231.png)

然后再使用git log 查看历史提交记录。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094240.png)

会发现add button 已经没有了，版本库已经回滚到add label提交的状态了，但是在我们add button 提交修改的文件 里面修改的内容没有丢失，只是回到了未提交的状态。

将文件再次提交，同样取名add button ，继续**git reset --mixed** 操作。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094254.png)

同样是回滚到了add button 之前的add label 提交。被修改的文件内容也没有丢失，但是修改的文件为红色了(未执行add 操作)。

将文件再次提交，同样取名add button ，继续进行**git reset --hard** 操作。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240311094303.png)

执行完git reset --hard 命令后，使用git status 查看文件状态，回滚到add label 提交，add button被修改的文件内容已经没有了，丢失了。版本库中的文件已经完全回到刚提交完add label时的状态。

git reset 根据需要使用不同的命令，使用 --hard 时一定考虑回滚后文件的丢失！


