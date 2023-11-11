- 4阶B+Tree
- 每颗节点最多有m棵子树
![image.png](https://iili.io/JfD8rRn.png)

- 非叶节点至少有两颗子树，其他每颗分支节点至少有$\lceil m/2 \rceil$棵子树
![image.png](https://iili.io/Jfb95rP.png)
- **节点的子树个数和关键字个数相等**
- 所有**叶子节点包含全部关键字**及指向对应记录（对应的数据）的指针。
- 叶子节点中将按关键字的大小顺序排列，并且**相邻叶子节点按大小顺序相互链接起来**。（支持顺序查找）
![image.png](https://iili.io/Jfb3ug2.png)
- 所有**分支节点**中仅包含它的各个子结点中的**关键字的最大值**及指向其子节点的指针。


### B+树的查找
#### 多路查找
- 查找一个9
- 因为9小于根节点的15，于是到15指向的分块，一个个匹配（从小到大，小于等于就进入），因为找到了9，（但查找并未结束，仍然进入叶子节点）
- 在689这个叶子节点当中匹配到9就结束了
![image.png](https://iili.io/Jfb0jKx.png)

- 查找一个7（失败）
- 先进15，再进9，689无从匹配，查找失败
![image.png](https://iili.io/JfbER24.png)


#### 顺序查找
从第一个叶子节点开始，一路往后找，顺序匹配
![image.png](https://iili.io/JfbhTG9.png)

### BTree对比B+Tree
1. ![image.png](https://iili.io/JfbhGG1.png)
 ![image.png](https://iili.io/Jfbh0ZB.png)
2. ![image.png](https://iili.io/JfbhS6X.png)
 ![image.png](https://iili.io/Jfbhswl.png)略有不同，几个关键字就几个指针B+Tree

3. ![image.png](https://iili.io/JfbhmFe.png)
 ![image.png](https://iili.io/JfbjRVI.png)

4. ![image.png](https://iili.io/Jfbjaln.png)
 ![image.png](https://iili.io/Jfbjbxp.png)


#### B+Tree和B树 比较（额外内容）
![image.png](https://iili.io/JfbNu4t.png)
- 读磁盘的效率是很低的，所以B+树的非叶子节点是不会保存关键字记录（完整信息）的。而Btree的节点都包含了关键字对应的记录的存储地址。
- 假设这个块只有1kb的大小，那么这个1kb应该尽可能存储索引的大小，而不是记录地址的大小，应该专门到一个地方统一放地址，这样子在存储节点的磁盘块这里能省出存储索引大小的空间。BTree3个关键字，4个指向子节点的指针，三个记录指针。B+Tree只有三个关键字，三个指向子节点的指针，部分节省了空间，能让一个磁盘块存储更多关键字，而排除掉记录指针的存储。
![image.png](https://iili.io/Jfbe821.png)

### 知识回顾
![image.png](https://iili.io/Jfb82d7.png)
