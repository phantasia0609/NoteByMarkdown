### 知识总览
![image.png](https://iili.io/JKpu2DX.png)

### 平衡二叉树的定义（一定是二叉排序树）
- 平衡二叉树(Balanced Binary Tree)，简称平衡树（AVL树，树名称来自于创造这个算法的人）
- 树上的任一节点的左子树和右子树的高度之差不超过1
- 左子树和右子树也都是平衡二叉排序树
- <mark style="background: #FFF3A3A6;">节点的平衡因子</mark> = 左子树高 -- 右子树高（只能为1，-1，0）
![image.png](https://iili.io/JKpumXe.png)


### 平衡二叉树的插入
**关键问题：** 在插入新节点之后，树如何保持平衡？
- 我们需要调整其中的 **“最小不平衡子树”** 
- 从插入点往上找，找到第一个不平衡的节点。
![image.png](https://iili.io/JKpAk4j.png)
- 可以调节成下图的样子
![image.png](https://iili.io/JKpRxt9.png)

### 调整最小不平衡子树
- 分为下面四种情况
- ![image.png](https://iili.io/JKpRtVe.png)
- ![image.png](https://iili.io/JKpNWfj.png)
- 比较好的记忆是 比较 ABC的大小，然后把中间的作为根节点

##### 先来举例一种情况
![image.png](https://s2.loli.net/2023/10/27/fNCDnU56WHzm9VJ.png)

### 调整最小不平衡子树（LL）
- 左子树过高
- A的左孩子的左子树导致的不平衡
- 由于A是最小不平衡子树，所以AR BL BR的高度应当一致，可以反证法证否
![JKpWi42.png](https://iili.io/JKpWi42.png)
- LL平衡旋转（**右单旋转**）由于BL < B < BR < A < AR
- B变为A的父节点，A作为B的右子树，而原来BR < A
- BR变为A左子树，AR仍然为A的右子树，
- 于是在这颗完整的子树内，不但继续保持了平衡，在父节点下仍旧保持了二叉搜索树的特性。
![image.png](https://iili.io/JKpXRyX.png)


#### 调整最小不平衡子树（RR）
- A是最小不平衡子树
- AL BL BR高度应当一致
- 最小不平衡子树的root节点balance小于-1，并且右子树过高
![image.png](https://iili.io/JKpXQPR.png)
- B变为根，A变为B的左子树，BL变为A的右子树，BR仍然为B的右子树，AL为A的左子树
![image.png](https://iili.io/JKpjmjn.png)
- 6 和 8就是RR
![image.png](https://iili.io/JKpOXQn.png)


**简单说一下LL和RR的代码实现思路**
![image.png](https://iili.io/JKpwT3Q.png)

#### 调整最小不平衡子树（LR）
- 情况展示
- 红色的小球是新增点
- ![image.png](https://iili.io/JKpe7uS.png)
- 归根结底是通过子树的大小关系来移动的
![image.png](https://iili.io/JKpk9NS.png)
- 当然这个新的节点插在c的左右其实不影响
![image.png](https://iili.io/JKpknRV.png)


#### 调整最小不平衡子树（RL）
看一下示例
![image.png](https://iili.io/JKpkWfs.png)
- 实际处理情况
![image.png](https://iili.io/JKpvz74.png)

- 当然这个节点插入在C的左右其实没什么区别
![image.png](https://iili.io/JKpvpZ7.png)
### 小总结
- 旋转的过程中是带着子树的，并且旋转是相对他的父节点而言，会替代其父节点的位置
![image.png](https://iili.io/JKp8YwN.png)


#### 填一个小坑，
- 图中过的问题是因为我们调整了 最小不平衡子树的高度
- 我们把最小不平衡子树的高度削减了1，所以会影响所有父节点的平衡因子。
![image.png](https://iili.io/JKpSTW7.png)

#### 小练习

RR
- 66为A，68为B ，70为C，右孩子左旋，B为中间大小，B左旋到66的位置，66作为68的左子树，67作为66的右子树，70仍然是68的右子树
![image.png](https://iili.io/JKpUEvf.png)


RL
50为A， 68为B，66为C，于是C先向右旋转，再向左旋转
![image.png](https://iili.io/JKpg2Fn.png)
结果如下
![image.png](https://iili.io/JKpgGKF.png)


LR
66为A，50为B，60为C，60先左旋，再右旋
![image.png](https://iili.io/JKpg1P1.png)

### 查找效率分析

![image.png](https://iili.io/JKprmBI.png)
![image.png](https://iili.io/JKp4CE7.png)

- 一个有9个节点的AVL树，其最大高度就是4，高度为5要求有12个节点至少。