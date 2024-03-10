B站评论案例
1. 渲染评论列表
2. 删除评论实现
3. 渲染导航Tab和高亮实现
4. 评论列表排序功能实现

Realization
#### 渲染评论列表
- 核心思路
	1. 使用useState维护评论列表
	2. 使用map方法对列表数据进行遍历渲染（记得加key）

#### 实现评论的删除
- 需求
	1. 只有自己的评论才显示删除按钮
	2. 点击删除按钮，删除当前评论，列表中不再显示
- 核心思路
	1. 删除显示-条件渲染
	2. 删除功能-拿到当前项的id，以id为条件对列表评论做filter过滤

![image.png](https://iili.io/JYWzxx2.png)

#### 渲染TAB + 点击高亮实现
- 需求：点击哪个tab项，哪个做高亮实现（最新 | 最热）
- 核心思路：点击谁就把谁的**type记录下来（标识）**，然后和遍历时的**每一项的type做匹配**，谁匹配到就设置负责高亮的类名
- ![image.png](https://iili.io/JYWSVJS.png)
- ![image.png](https://iili.io/JYWSW57.png)


#### 排序功能实现
- 需求：点击最新，评论列表按评论时间排序，最热按点赞数拍虚
- 核心思路：把**评论列表状态数据进行不同的排序处理**，当成新值传给set函数重新渲染视图UI

`可以尝试使用Lodash（库）的order方法`[lodash.orderBy | Lodash中文文档 | Lodash中文网 (lodashjs.com)](https://www.lodashjs.com/docs/lodash.orderBy#_orderbycollection-iteratees_identity-orders)`
- ![image.png](https://iili.io/JYWpyKB.png)
- 这里是优先对user参数进行升序排序，其次根据age参数进行降序排序

#### classnames优化类名控制

 *classnames介绍*
- classnames是一个简单的js库。 可以非常方便的**通过条件动态控制class类名的显示**
- 现在的问题：字符串的拼接方式不够直观，也容易出错
- 下图是使用classnames库所进行的操作
- ![image.png](https://iili.io/JYXFFdQ.png)

#### 发表评论功能
- 核心步骤
	1. 获取评论内容
	2. 点击发布按钮发布评论
	3. id处理和时间处理
![image.png](https://iili.io/JYSjCUG.png)

#### 评论id唯一处理和当前时间格式处理的方法
- 1. rpid要求一个唯一的随机数id - 使用**uuid**库
- 2. ctime要求以当前时间为标准，生成固定格式 - **dayjs**库
![image.png](https://iili.io/JYSjqfn.png)


#### 评论后内容清空并重新聚焦
1. 清空内容 - 把控制input框的value状态设置为空串
2. 重新聚焦 - 拿到input的dom元素，调用focus方法，让当前的focus在inputRef绑定的DOM元素上。
``` js
						inputRef.current.focus()
```
![image.png](https://iili.io/JYSjKiX.png)

## 包的导入
![image.png](https://iili.io/JazC0Ft.png)

### 优化需求
#### 1. 使用请求接口的方式获取评论列表并渲染
- 1. 使用**json-server**工具模拟接口服务，通过**axios**发送接口请求
	-  json-server是一个快速以.json文件作为数据源模拟接口服务的工具
	- axios是一个广泛使用的前端请求库
	- ![image.png](https://iili.io/JaSDxDX.png)


#### 2. 使用自定义Hook函数封装数据请求的逻辑
- 一般思路
	1. 编写一个use开头的函数
	2. 函数内部编写封装的逻辑
	3. return出去组件中用到的状态和方法
	4. 组件中调用函数解构赋值使用
	![image.png](https://iili.io/JaUA51s.png)

#### 3. 把评论中的每一项抽象成一个独立的组件实现渲染
![image.png](https://iili.io/JaUWPp9.png)

- 子组件
- ![image.png](https://iili.io/JaUWQLb.png)
- 父组件
- ![image.png](https://iili.io/JaUWDEx.png)
