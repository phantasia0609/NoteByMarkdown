
--- 
最小生成树的概念
---

#### 生成树 
>![image.png](https://s2.loli.net/2023/10/23/CL1wftDAVOku2rd.png)

#### 最小生成树（MST/最小代价树）权值最小
>![image.png](https://s2.loli.net/2023/10/23/DReUKhkQ4dpmt7X.png)
>
>![image.png](https://s2.loli.net/2023/10/23/z8lhrstpcjfRDH3.png)
>
>- 如果一个连通图本身就是一棵树，那么其最小生成树就是它本身
>- 只有连通图才有生成树，非连通图只有生成森林
>
>![image.png](https://s2.loli.net/2023/10/23/d4z6EigprKyHhOk.png)


## Prim算法 
[最小生成树——Prim算法（详细图解）_prim最小生成树_skynesser的博客-CSDN博客](https://blog.csdn.net/qq_62213124/article/details/121597780)

## Kruskal算法 
[最小生成树之 Kruskal 算法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/455640440)

## Prim+Kruskal
[算法最小生成树——Prim和Kruskal算法-CSDN博客](https://blog.csdn.net/weixin_44333151/article/details/110584056)

> 最大生成树的算法，可以先让所有的权值取负数，又变成了最小生成树。

---
先来介绍Prim算法
---
>- 算法的核心是 从某一个顶点开始构建生成树，
>- 每次将代价最小的新顶点纳入生成树并且是不会生成环的（代价最小是<mark style="background: #FFB86CA6;">未被纳入的顶点</mark>相对当前树而言的）
>- 直到所有顶点都纳入为止
>
>~~必须要说明的是：Prim算法是一个贪心算法，它不一定能求得理论上的最好结果~~

- 我们以下图这个例子的完整流程来证明一下
![image.png](https://s2.loli.net/2023/10/23/EFdBwrIpWykjaLX.png)
- 由于我们的起始点 是P城， 权值最小的边是学校，故要把学校纳入到当前的生成树来，生成树变成了如下的样子
![image.png](https://s2.loli.net/2023/10/23/9IYyw6gceLv3pbM.png)

- 此时找到下一个距离 当前树 的权值最小的点
- 很明显此时有两个选项 矿产和渔村 （这两个是任选的）
![image.png](https://s2.loli.net/2023/10/23/KJNYe7QsAybMLwl.png)
- 再下一个是渔村，因为渔村和矿产之间的权值仅仅只有2
 ![image.png](https://s2.loli.net/2023/10/23/bysAmwR6MNi3JEP.png)
- 然后便是农场连接P城  电站连接农场
 ![image.png](https://s2.loli.net/2023/10/23/bxMvuBlTtHKEPQh.png)


> 如果在上面我们选择p城 先连接 渔村，则会得到另一个最小生成树
> ![image.png](https://s2.loli.net/2023/10/23/5XAWPIcortdnZlU.png)

#### Prim 算法的实现思想
- lowCost是**存储 未加入树的节点 和树这个整体 的连接的最小权值**
- 当第一步选取$V_0$的时候，剩下的点的lowCost是需要更新第一遍的，如图所示，并且其中的最小值是$V_3$的lowCost
![image.png](https://iili.io/JK5rPwv.png)

- 选取好$V_3$之后需要更新LowCost，只有目前的LowCost值更小，才更新这个节点的LowCost值
- 由于只遍历没有加入树的点，所以$V_3$的lowCost是没有 也不必要更新的
![image.png](https://iili.io/JK5Pd4S.png)
>- 当前lowCost中未加入树的最小的权值是4，由于顺序遍历，则加入树的的点应当就是$V_2$，并且更新权值的点是根据$V_2$来的，也就是说每次加入新节点之后，lowCost是 **根据这个新加入的节点** 和 **未加入树的节点** 之间的边的权值 与**原来的lowCost数组中的数比较**，从而替换or不改变。

- 那么加入的$V_2$只与$V_5$相连，并且是遍历$V_2$相连的点找到的边，所以更新的时候是更新$V_5$的lowCost
![image.png](https://iili.io/JK5shQf.png)

#### 时间复杂度
![image.png](https://iili.io/JK5ZKIn.png)


#### 与Kruskal算法的比较
![image.png](https://iili.io/JK5gTej.png)




代码如下
```cpp
#include <iostream>

#include <climits>

  

#define V 5  // 图中顶点的数量

  

// 从未被包含在最小生成树中的顶点中找到具有最小键值的顶点的索引

int minKey(int key[], bool mstSet[]) {

    int min = INT_MAX, min_index;

  

    for (int v = 0; v < V; ++v) {

        //找到所有未接入的顶点当中与 生成树 的点的连接的权值最小的点 把他加入生成树

        if (!mstSet[v] && key[v] < min) {

            min = key[v];

            min_index = v;

        }

    }

  

    return min_index;//没有进入if 的话，这个默认是0

}

  

// 打印最小生成树的边和权重

void printMST(int parent[], int graph[V][V]) {

    std::cout << "Edge \tWeight\n";

    for (int i = 1; i < V; ++i) {

        std::cout << parent[i] << " - " << i << "\t" << graph[i][parent[i]] << "\n";

    }

}

  

// 执行Prim算法来找到最小生成树

void primMST(int graph[V][V]) {

    int parent[V];      // 存储最小生成树中的父节点

    int key[V];         // 存储顶点的键值（与当前最小生成树的连接权重）

    bool mstSet[V];     // 记录顶点是否包含在最小生成树中

  

    // 初始化所有顶点的键值为无穷大，将它们都标记为未包含在最小生成树中

    for (int i = 0; i < V; ++i) {

        key[i] = INT_MAX;

        mstSet[i] = false;

    }

  

    key[0] = 0;         // 从第一个顶点开始构建最小生成树

    parent[0] = -1;     // 第一个顶点没有父节点

  

    // 构建最小生成树，总共执行V-1次循环

    for (int count = 0; count < V - 1; ++count) {

        int u = minKey(key, mstSet);    // 从未包含在最小生成树中找到键值最小的顶点

        mstSet[u] = true;               // 将该顶点标记为已包含在最小生成树中

  

        // 更新与当前顶点相邻的顶点的键值

        for (int v = 0; v < V; ++v) {

            //1.存在边 2.未访问 3.比上一个得到的最小权值小  （弊端就是每次只更新新加入的节点的权值）

                                                        // 这不是实时更新全部的

            if (graph[u][v] && !mstSet[v] && graph[u][v] < key[v]) {

                parent[v] = u;

                key[v] = graph[u][v];

            }

        }

    }

  

    printMST(parent, graph);  // 打印最小生成树的边和权重

}

  

int main() {

    int graph[V][V] = {

        {0, 2, 0, 6, 0},

        {2, 0, 3, 8, 5},

        {0, 3, 0, 0, 7},

        {6, 8, 0, 0, 9},

        {0, 5, 7, 9, 0}

    };

  

    primMST(graph);  // 调用Prim算法来寻找最小生成树

  

    return 0;

}
```