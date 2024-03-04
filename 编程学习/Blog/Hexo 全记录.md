#hexo #blog
## 安装 Hexo Cli

```
npm i -g hexo-cli
```
## 如果是 mac or linux 
![image.png](https://iili.io/JMpaOTN.png)
```
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```
## 如果是 windows 
> 执行 hexo 命令时应当添加前缀

```
npx hexo -v
npx hexo cl
npx hexo init
npx hexo g
npx hexo s
```

## 验证安装
```
hexo -v
```

## 指定目录（空目录）
```
hexo init
```
> 得到下面的目录
![image.png](https://s2.loli.net/2024/03/02/MGdm28LU5PhcNnI.png)

## 配置主题
```
	git submodule add theme地址 themes/地址名称 
```
![image.png](https://s2.loli.net/2024/03/02/tMS4sguEkjXFGnU.png)

## 修改_config.yml 文件
> 修改 theme 选项为自己的主题名称
![image.png](https://s2.loli.net/2024/03/02/1mg983oZEQSeqya.png)

##  hexo 指令
```
	hexo cl
	hexo g
	hexo s
```

## 启动成功