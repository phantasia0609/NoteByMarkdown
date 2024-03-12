查看 shell 类型
可以执行命令 `echo $SHELL`，先查看终端类型。
`bash: /bin/bash`
`zsh: /bin/zsh `

shell 类型切换命令
切换到 bash
输入命令：`chsh -s /bin/bash`

切换到 zsh
输入命令：`chsh -s /bin/zsh `

注意需要重启终端生效（强制退出后再打开）

遇到个问题：无法正常使用/usr/libexec/java_home -V，就是 shell 的问题，必须切换到 zsh 才行

shell 是一种脚本命令解释器，有 bashell、zshell、cshell 等，bashell 是 Mac OS 默认的 shell，欲知详情可以点击下方链接查看：
[什么是 shell？][http://c.biancheng.net/view/706.html]

chsh: no changes made
[解决方法一][https://www.bilibili.com/video/av 245404070/]

解决方法二:
1、我们都知道 mac 有默认 bash 工具，在下载 zsh 后，把一切都配置好后，输入切换命令：`chsh - s /bin/zsh` ,总是提示 `chsh: no changes made` 错误。那就尝试用 `sudo chsh -s /bin/zsh` 再试一次。如果还是不行，就不用再弄了，直接用下面的方法吧！
终端输入：
```
dscl . -read /Users/$USER/ UserShell
exec su - $USER
```

然后输入密码即可完美解决~
欲知 chsh 命令请点击下方链接查看：
[chsh 命令详解][https://www.runoob.com/linux/linux-comm-chsh.html]
