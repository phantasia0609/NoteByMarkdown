#### 回归：二叉查找树（BST）
- 用一个关键字，把搜索范围减半
![image.png](https://iili.io/JfjvJqb.png)

- **那能不能把这颗树变成m叉查找树呢？**
- 以5叉查找树为例
![image.png](https://iili.io/JfjSIJR.png)

- 在当前Node结构体内遍历key，找到当前的查找值在key中的哪些值之间，或之外，然后根据key值跳跃到下一个Node中
![image.png](https://iili.io/JfjUoQ9.png)

- 查找失败的例子
![image.png](https://iili.io/JfjU4yl.png)

### 如何保证BTree的查找效率
- 策略：m叉查找树中，规定**除根节点外**，任何非叶节点**至少有$\lceil m/2 \rceil$个分叉**，即**至少含有$\lceil m/2 \rceil$-1个关键字**。（前面两个是向上取整。
![image.png](https://iili.io/Jfjgo9R.png)
- 除根节点外，是因为根节点在节点过少的时候根本做不到，其实节点过少的时候，其他节点叶做不到（但是如果加上非叶节点的话就没问题了）

- 但如果出现下图的话，由于不够“平衡”，效率仍然不够高
- 于是，需要规定：**任何非叶节点，其所有子树的高度都需要相同**
![image.png](https://iili.io/Jfj6ZDQ.png)


### B Tree的完整定义
- B树，又称多路平衡查找树，B树中所有节点的孩子个数的最大值成为B树的阶，通常用m表示。一颗m阶B树或为空树，或为满足以下特性的树：
>1. 树中每个节点至多有m棵子树，即至多含有m-1个关键字
>2. 若根节点不是终端节点，则至少有两棵子树。
>3. **除根节点外**的所有非叶节点**至少有$\lceil m/2 \rceil$棵子树**（终端节点的叶子节点其实就是空节点），即**至少含有$\lceil m/2 \rceil$-1个关键字**。
> 4. 所有的<mark style="background: #D2B3FFA6;">叶节点</mark>都出现在同一层次上，并且不带信息（可以视为外部节点，或类似于折半查找判定树的查找失败节点，实际上这些结点不存在，指向这些节点的指针为空。
> 5. 所有的非叶节点的结构如下
>
>| n   | $P_0$ | $K_1$ | $P_1$ | $K_2$ | $P_2$ | $\dots$ | $K_n$ | $P_n$ |
>| --- | ----- | ----- | ----- | ----- | ----- | ------- | ----- | ----- |
>- 其中Ki（i=1，2，...,n)为节点的关键字，且满足K1 < K2 < ... < Kn; Pi（i=0,1,...,n)为指向子树根节点的指针，且指针Pi-1所指子树中所有节点的关键字均小于Ki，Pi所指子树中所有节点的关键字均大于Ki，n($\lceil m/2 \rceil$ - 1 $\le$ n $\le$  m-1)为节点中关键字的个数
>![image.png](https://iili.io/Jfjy3og.png)
>![image.png](https://iili.io/JfjyxRI.png)

#### 核心特性
- 根节点可以有多个节点，比如只有两个节点的时候，就可以这么干。
![image.png](https://iili.io/Jfjy7ff.png)


### B树的高度
- 最小高度（对于n个关键字m阶btree）
- 让每个节点尽可能填满（**根节点也可以填满**），也就是每个节点都有m-1个关键字，于是每一层分别由1，m，m平方,...节点
- 所以如图（小于等于，大于等于号均改成等于号，因为这就是最小高度）
  ![image.png](https://iili.io/JfwJUX9.png)

- 最大高度（对于n个关键字m阶btree）
- 每层的分叉尽可能少（**根节点只有2个分叉**），分叉只有$\lceil m/2 \rceil$个，每个节点关键字只有$\lceil m/2 \rceil$-1个，则第一层1个节点，第二层2个节点，第三层2$\lceil m/2 \rceil$个，第h层2${\lceil m/2 \rceil}^{h-2}$个关键字。那么h+1层（叶子节点层）有2${\lceil m/2 \rceil}^{h-1}$个节点。
- 由于n个关键字的Btree一定由n+1个叶子节点（失败节点，就是n个关键字把数轴分成了n+1个区间），则最大的时候，n+1 = 2${\lceil m/2 \rceil}^{h-1}$，于是如图
![image.png](https://iili.io/Jfw3j0g.png)

- 最大高度的最少节点数，最少关键字数
![image.png](https://iili.io/JfwFUyx.png)
 - 于是可以得到h层的m阶B树至少含有的关键字个数
 - 关键字总数一定是n，所以这个情况下只是得到了b树的最大高度，下图中的不等号改为等号。
 ![image.png](https://iili.io/Jfw5rAB.png)

- 总之，可以得到B树的最小高度和最大高度
![image.png](https://iili.io/JfwY7Bn.png)


### 知识回顾与总结
![image.png](https://iili.io/Jfwcsbp.png)


B树 Balance查找树。 