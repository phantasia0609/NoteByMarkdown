#### 各顶点间的最短路径、带权、无权

- **Floyd算法思想介绍**
- 每一步都是当前最优
- 即便不为当前最优，也能让部分最优，完成部分路径的最优，总能得到整体最优
- 意思就是说 我能接着利用 我之前得到的 部分最优
![image.png](https://iili.io/JKYJTRj.png)

#### 模拟一下Floyd算法的执行过程

>- 初始状态
>- 就目前的已有边来看，各个顶点之间的最短的路径长度，这里就是有向边的权值
>- 初始状态没有中转点，全部设置为-1
>![image.png](https://iili.io/JKYJZdu.png)
>
>- 如果我们用$V_0$作为中转点，执行图中的运算，就会得到$V_{2}\to V_{1}$的一条路，他是经过$V_0$的
>- 上标k就是第k次去完整循环这个二维矩阵的所有元素
> ![image.png](https://iili.io/JKYqkCv.png)

>- 如果允许从$V_0$和$V_1$中转，也就是说现在的矩阵是执行过$V_0$中转之后得来的
>![image.png](https://iili.io/JKYCyhu.png)

>- 如果允许在$V_0$、$V_1$、$V_2$中转，在$V_0$、$V_1$中转的基础上得到。
>![image.png](https://iili.io/JKYngaV.png)

- 于是得到了一个较为简单的图的一些最短路径
![image.png](https://iili.io/JKYoRPj.png)
![image.png](https://iili.io/JKYoSxn.png)


**为什么说是简单的实现呢？**
因为，如果四个节点，两个中转，上述分析便不再正确。

**但是，这张图片的代码是正确的**
- 代码中完整遍历了从哪个点起始这么回事
![image.png](https://iili.io/JKYoSxn.png)


**那么，来考虑一个复杂情况**
- 这第一步没什么意义，因为V0没有入度，其本身就不能作为中转点。
![image.png](https://iili.io/JKYIItt.png)

- 第二步
![image.png](https://iili.io/JKYTAmB.png)

- 第三步
- 这里已经可以看出来了，V2到V3原来是没有边的，我们利用了V1这个中转点，所以V0到V3从V2中转，实际上也用上了V2和V1两个中转点，这个就是把中转点加入顺序给逆过来了
- 就是虽然我当前有这么个路径
- 如果我后续添加中转的时候，由于我是遍历整个二维数组，所以我就有办法利用上这个新的中转点
![image.png](https://iili.io/JKY5r8b.png)

- 第四步
![image.png](https://iili.io/JKY7Yle.png)

- 第五步
![image.png](https://iili.io/JKY7wUg.png)


找完整路径（太jb抽象了）
![image.png](https://s2.loli.net/2023/10/23/rTftwqHy13e6lOp.png)



小练习
![image.png](https://s2.loli.net/2023/10/24/PAgtnqTOB1GNSLv.png)

不能解决的问题
![image.png](https://s2.loli.net/2023/10/24/7N24bCLuFcHJwij.png)



---
总结
---
![image.png](https://iili.io/JKY0j9e.png)

