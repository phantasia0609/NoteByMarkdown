一：什么是 Anaconda？
Anaconda 可以便捷获取包且对包能够进行管理，同时对环境可以统一管理的发行版本
Anaconda 包含了 conda、Python 在内的超过 180 个科学包及其依赖项，包括 conda、pip、numpy、scipy、ipython 等

二：安装步骤
——Anaconda 官网下载命令行安装包： https://www.anaconda.com/products/individual#macos



——安装 Anaconda
```
bash ～/后面跟上下载的路径
bash ~/Downloads/Anaconda 3-5.0.1-MacOSX-x 86_64.sh
```
——根据终端的提示步骤进行安装，当看到“Thank you for installing Anaconda!”则说明已经成功完成安装
关闭终端，然后再打开终端以使安装后的 Anaconda 启动


——配置环境变量
```
//使用命令 open .bash_profile 打开配置文件
open .bash_profile 或 open -e .bash_profile
 
//在配置文件末尾添加路径
export PATH=~/anaconda 3/bin:$PATH
 
//编译系统配置文件
source ~/.bash_profile
```


三：常用命令
>——查看 Conda 版本：conda --verison
>——查看已经安装的包名和版本号：conda list
>——更新 Conda 到最新版本：conda update conda
>——查看当前存在哪些虚拟环境：conda env list
>——查看 Conda 配置：conda config --show
>——恢复默认源：conda config --remove-key channels
>——净化 Conda：conda clean -a 或 conda clean -i
>——删除 Anaconda：conda install anaconda-clean
>——创建虚拟环境：conda create -n your_env_name python=X.X
>——激活某个虚拟环境：conda activate your_env_name
>——删除某个虚拟环境：conda remove -n your_env_name --all
>——关闭虚拟环境：conda deactivate

四：更换源解决更新或下载慢的问题
——查看当前 Conda 配置：正常情况下都为国外的默认源


conda config --show
1.
——添加国内镜像源：
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
```


——再次查看 Conda 配置：添加了一个新的镜像源


复制 
conda config --show

——打开用户目录下的 .condarc 文件并删除掉 default 


open ~/.condarc

——再次查看 Conda 配置：若只有国内镜像源没有 default 国外默认源即为替换成功

-----------------------------------
©著作权归作者所有：来自 51 CTO 博客作者 mb 60 e 5417 d 375 b 8 的原创作品，请联系作者获取转载授权，否则将追究法律责任
Mac 安装 Anaconda
https://blog.51cto.com/u_15296378/4969328