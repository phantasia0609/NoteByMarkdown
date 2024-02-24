#### 带权、不带权、单源

##### BFS算法的局限性
- 下图中G到R的最短距离是G到P再到R，BFS可做不到如此搜索
![image.png](https://iili.io/JK7k1fe.png)

#### Dijkstra算法演示
- final标记着各个顶点是否已经找到最短路径
- dist（distance）表示当前节点在 **已经遍历路径** 的上的长度
- path表示路径的直接前驱
- ~~这个算法与Prim算法十分相似~~

>- 先进行这个处理，不进入循环
>- $V_0$作为起始点，第一个路径先去索引$V_1$
>- 路长度为10，但仅有此一条路，所以设置dist为10，前驱为0
>![image.png](https://iili.io/JK78cFe.png)
>- 第一轮循环（在这里作为循环起始点）方便后续判断如果顶点全部遍历就可以退出了）
>- 如果第一轮循环没有确定最短路径，则将第一轮循环中dist最小的顶点的最短路径长度确定下来
>- 让此节点final变为true，图中为$V_4$
>![image.png](https://iili.io/JK7r8gt.png)
>- 由于已经有了$V_4$的dist信息，通过遍历剩余的节点，如果有$V_4$指向该节点的路
>- 那么便计算 **$V_4$到当前节点的距离 加上 $V_4$本身的distance** 并且和原来的distance做比较，如果比原来的distance小，则更改（从这里能体会到贪心的感觉了，并不一定是最优解）
>![image.png](https://iili.io/JK7PosR.png)

>- **进入第二次循环**
>- 遍历节点，让dist最小的点的final设置为true
>![image.png](https://iili.io/JK7Pls4.png)
>
>- 然后由于已经有了$V_3$的dist信息，通过遍历剩余的节点，如果有$V_3$指向该节点的路
>- 那么便计算 **$V_3$到当前节点的距离 加上 $V_3$本身的distance** 并且和原来的distance做比较，如果比原来的distance小，则更改（从这里能体会到贪心的感觉了，并不一定是最优解
> - **没有再去判断前面两个点了**
> 如图
> ![](https://iili.io/JK7iBY7.png)


>- **第三轮循环**
>![image.png](https://iili.io/JK7iP87.png)
>![image.png](https://iili.io/JK7iZZb.png)


>**第四轮循环（结束）**
>![image.png](https://iili.io/JK7s3wg.png)


>- 结束后可以进行的一些操作
>- 路径长度
>- 路径完整表示
>![image.png](https://iili.io/JK7s5oG.png)


#### Dijkstra算法的时间复杂度
- 初始化操作（相当于循环先进行了一次，对初始节点的子节点path值赋值，初始节点final设为true，path为-1，dist为0.
- n-1轮处理
- 每一轮处理都是扫描所有数组找distance最小的顶点O（n），还需要这个顶点指向的其他顶点，通过路径长度判断修改dist和path，这里还有一个O(n)，合起来也还是O(n).
 ![image.png](https://iili.io/JK7sifR.png)


#### 对比Prim算法
![image.png](https://iili.io/JK7QmPf.png)

#### 负权值带权图的不可用性
- 会先去V2后去V1，那V2自然少了一个更好的节点
![image.png](https://iili.io/JK7Ds9V.png)
