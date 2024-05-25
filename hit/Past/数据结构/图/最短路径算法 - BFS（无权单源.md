
- 先看一下目录
![image.png](https://iili.io/JK7Bh1p.png)

- BFS求无权图的单源最短路径
![image.png](https://iili.io/JK7Cyts.png)

- 遍历完之后可以得到路径长度
![image.png](https://iili.io/JK7nmgV.png)
- 具体算法可以动BFS代码改造出来
- 先看一下BFS代码
![image.png](https://iili.io/JK7oALG.png)

- 需要有一些更改
- d[]数组代表 从初始起点 到该节点的距离
- path[]数组代表 当前路径上该节点的直接前驱
![image.png](https://iili.io/JK7ukX9.png)

- 模拟一下代码的执行
- Dequeue出队列的时候会弹出一个节点，用u接收
- d[w] = d[u] + 1；//d[u]是从当前节点 w是从u出发的子节点，d[u]是距离起始点的长度，所以d[w]是d[u]+1
- path[w]是直接前驱，w的直接前驱是u
- 2号顶点有1，6两个孩子，1、6分别按下图内的数据设置好。然后进入1孩子
![image.png](https://iili.io/JK71hGV.png)

![image.png](https://iili.io/JK7MJpe.png)

![image.png](https://iili.io/JK7ML8P.png)

![image.png](https://iili.io/JK7OB7R.png)

- 其实就是对BFS的修改，添加了路径长度数组d，以及直接前驱数组path
- path方便我们从一个节点往前索引到完整路径
![image.png](https://iili.io/JK7OMBe.png)

