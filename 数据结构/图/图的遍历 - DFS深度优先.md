

#### 首先复习一下树的深度优先遍历
![image.png](https://s2.loli.net/2023/10/19/LiNoVexJ2SMs7mB.png)


#### 类比图的深度优先遍历
![image.png](https://s2.loli.net/2023/10/19/p2XkLWTjdU4ICBn.png)

>- 接下来模拟以下调用过程（递归实现）
>
>- ![image.png](https://s2.loli.net/2023/10/19/U3z17wXliOIPCNW.png)
>- ![image.png](https://s2.loli.net/2023/10/19/PGCKTmEAJVSUglQ.png)
> - ![image.png](https://s2.loli.net/2023/10/19/XGyA1of4IwajzUL.png)
>- ![image.png](https://s2.loli.net/2023/10/19/XqG6MnYfE9goBrS.png)
>- ![image.png](https://s2.loli.net/2023/10/19/wULgm8uPBiVlG2Q.png)
>- ![image.png](https://s2.loli.net/2023/10/19/zgho89aeVWRsyx7.png)
>- ![image.png](https://s2.loli.net/2023/10/19/1vyZPMdJWYKDION.png)
>- ![image.png](https://s2.loli.net/2023/10/19/uYHw3TLCNIBWokO.png)
>- ![image.png](https://s2.loli.net/2023/10/19/N4QmiYtoZyaFwq2.png)
>- ![image.png](https://s2.loli.net/2023/10/19/Kpfgr1WJLhF2D4i.png)
>到现在为止所有的顶点都遍历完了，逐步返回上一层
>- 先返回到7号 然后4号....


#### 算法存在问题(只能完成连通图)
![image.png](https://s2.loli.net/2023/10/19/v8hXY5mi4sUaA3R.png)
#### 算法的修改
![image.png](https://s2.loli.net/2023/10/19/tOzwrLIm7CbUZ14.png)

#### 算法的时空复杂度
>空间复杂度只看算法当中新开的空间，这里主要是栈空间
>
>![image.png](https://s2.loli.net/2023/10/19/NDIdFxEVgf6srTo.png)

>时间复杂度
>![image.png](https://s2.loli.net/2023/10/19/HTbOdKRx1gnAfZ9.png)

#### 遍历序列示例
![image.png](https://s2.loli.net/2023/10/19/RFe9LSbZxNKjqtJ.png)
从1号开始是 1 2 6 3 4 7 8 5


邻接表的不唯一性同样会导致优先遍历序列的不同
![image.png](https://s2.loli.net/2023/10/19/R4wpebY8l6WPOUm.png)


#### 深度优先生成树/森林

![image.png](https://s2.loli.net/2023/10/19/2w1M8piObozCkPB.png)

![image.png](https://s2.loli.net/2023/10/19/4gpvwH9WRf2rc6J.png)

#### 图的遍历和连通性
- 无向图
![image.png](https://s2.loli.net/2023/10/19/EfetoDRd94amXjq.png)

- 有向图
 ![image.png](https://s2.loli.net/2023/10/19/puaH4femGC16SQ2.png)



---
小结
---
![image.png](https://s2.loli.net/2023/10/19/x1el4aDKCuk2Wbg.png)
