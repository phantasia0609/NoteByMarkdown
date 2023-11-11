
# 广度优先遍历（BFS)

#### 参考树的广度优先遍历（其实就是层序遍历）
![image.png](https://s2.loli.net/2023/10/19/WV6Cs9FJpHkgZ5K.png)

>如果是图的广度优先遍历 假设起始位置为2 则 遍历顺序为 2    1/6   5/3/7   4/8
>其中 /分隔不分顺序
>
>![image.png](https://s2.loli.net/2023/10/19/Ezc1fxCiU5aD3oy.png)



#### 树和图的遍历实际上是有区别的
![image.png](https://s2.loli.net/2023/10/19/BMDryAdUZJGqPnI.png)
>为了解决搜索到已访问的问题， 可以设立一个搜索到的标志


#### BFS代码实现
![image.png](https://s2.loli.net/2023/10/19/ZajMGWR4hTts6zg.png)


>- 假设从2开始
>- 这个出队列DeQueue理应会返回一个值被v接受
>- 然后下面的for循环才是对当前节点的处理
>
>![image.png](https://s2.loli.net/2023/10/19/6SVnXAsNeo9ZKwy.png)
>
>![image.png](https://s2.loli.net/2023/10/19/bA5IvceaiDxOpWS.png)
>
>![image.png](https://s2.loli.net/2023/10/19/u7jwVJtL2nOdoas.png)
>
>![image.png](https://s2.loli.net/2023/10/19/kASF14J8HsiW3Ym.png)


>如果采用邻接表存储，广度优先遍历的顺序是可变的
>![image.png](https://s2.loli.net/2023/10/19/5ZJGsPxAcm7rWVD.png)


#### 算法存在的问题
> 算法只能找到联通图中的所有节点，如果是非连通图将无能为力。
>![image.png](https://s2.loli.net/2023/10/19/9zc4p6vedYsVmTx.png)
 
#### 增加一个遍历visited数组，判断是否全为true，否则就从不为true的地方重新开始bfs 
>也就是if(！visited[i])  BFS(G,i);这一段代码  调用BFS的次数也就是连通分量的个数
>![image.png](https://s2.loli.net/2023/10/19/KckFjGUSlfNvemH.png)

#### BFS的时空复杂度
>不要钻牛角尖，因为不同的实际结构以及存储结构会带来代码复杂度的较大差异
>所以在计算时间复杂度的时候
>我们只考虑<mark style="background: #D2B3FFA6;">计算 访问节点 以及 寻找边</mark> 这两个步骤的次数就好了


>- 空间复杂度（我觉得他说得不对，因为那个visited数组也得算上
>- 以及存储结构为什么不算上呢？
>- 不钻牛角尖，只看算法中新开的空间大小（辅助队列）
>
>![image.png](https://s2.loli.net/2023/10/19/6LVBAsNgqT4zdb7.png)

>时间复杂度 
>- 邻接矩阵
>
>![image.png](https://s2.loli.net/2023/10/19/R3niUYrV5HuKNIs.png)
>
>- 邻接表
>
>![image.png](https://s2.loli.net/2023/10/19/fyYoS3C5AFTujka.png)

#### 广度优先生成树
- 节点的访问顺序并不固定
![image.png](https://s2.loli.net/2023/10/19/Hc4b8iMGlEKDOuY.png)


- 邻接表得到的广度优先生成树不唯一
![image.png](https://s2.loli.net/2023/10/19/WS8P32OEiGrJsHT.png)


#### 广度优先生成森林
![image.png](https://s2.loli.net/2023/10/19/l9vzDCrWZNh6QmY.png)

#### 有向图的BFS过程
![image.png](https://s2.loli.net/2023/10/19/K1PAbtpLnjgE9Wl.png)
答案是4和1，firstneighber 和 nextneighber都是有向的弧，所以只能找到出度


---
小结
---
![image.png](https://s2.loli.net/2023/10/19/YmJyId7VZFulEP9.png)
