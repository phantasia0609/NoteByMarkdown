
---

- 接着Prim算法，现在我们来看Kruskal算法。
- 与Prim算法相同的是，Kruskal算法也是一种贪心算法，仍然不能在所有情况当中都得到最理想的答案。
#### 与Prim算法不同的是，Kruskal算法注重的是边，而不是点
> Prim算法一直在找和当前树 未连接的点 中权值最小的点，所以每次 添加一个点到树当中，就需要重新更新剩下点与树连接的最小权值，然后再找这些权值中的最小权值，反复执行。

- 找当前图中权值最小的边，这里是P城和学校之间的道路
![image.png](https://iili.io/JK5N5pS.png)

- 由于我们是按边添加的，这次就是一次添加了这条边，显示在我们添加了两个节点，当然后续的添加不一定是两个点了
![image.png](https://iili.io/JK5OLOB.png)

- 剩下的图中的权值最小的边是2 、 3 ![image.png](https://iili.io/JK5kg8x.png)

- 此时再找剩下的边当中的权值最小的边，是两条权值为4的边
 ![image.png](https://iili.io/JK5viJf.png)

- 由于我们每次找边的时候，一定要确定***原来这 条边连接的两个点 是否连通*** 如果不连通才可以取，连通是不可以选择的。所以剩下的这个权值为4的点不可以取
![image.png](https://iili.io/JK5Su3u.png)

- 然后便是找 权值为 5的顶点，同样有两个，但由于限制，只能取其一，然后连通、结束
![image.png](https://iili.io/JK5S49f.png)

#### Kruskal实现思想
- 所有的边都按照权值排序好
- 每次都弹出一个当前权值最小的边，只要没有环，就给他加入进去
![image.png](https://iili.io/JK7Js6X.png)

- 按规则继续连 ![image.png](https://iili.io/JK7dSf9.png)

#### 时间复杂度
![image.png](https://iili.io/JK73b9a.png)

#### 比较一下 Prim 算法和 Kruskal算法
![image.png](https://iili.io/JK5gTej.png)



#### 代码实现
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std；
// 定义图的边
struct Edge {
    //  起始  结束  权重
    int src, dest, weight;
};
// 定义并查集的数据结构

class UnionFind {

public:

    UnionFind(int n) {

        //初始化两个容器 rank是记录 当前数的高度的，为高效合并两个树做准备

        parent.resize(n);

        rank.resize(n, 0);

        for (int i = 0; i < n; ++i) {

            parent[i] = i; // 初始时，每个节点的父节点是自身

        }

    }

  

    int find(int x) {

        if (x != parent[x]) {

            parent[x] = find(parent[x]); // 使用路径压缩来加速查找操作

        }

        return parent[x];

    }

  

    void unionSets(int x, int y) {

        int rootX = find(x);

        int rootY = find(y);

  

        if (rootX != rootY) { // 如果x和y不属于同一个集合

            if (rank[rootX] < rank[rootY]) {

                parent[rootX] = rootY; // 将rank较小的树连接到rank较大的树上

            } else if (rank[rootX] > rank[rootY]) {

                parent[rootY] = rootX;

            } else {

                parent[rootY] = rootX;

                rank[rootX]++; // 如果rank相等，将其中一个树的rank增加1

            }

        }

    }

  

private:

    vector<int> parent;

    vector<int> rank;

};

  

// 自定义比较函数，用于对边按权重进行排序

bool compareEdges(const Edge& a, const Edge& b) {

    return a.weight < b.weight;

}

  

// Kruskal算法实现

// 永远是根据边的权值来做这些东西，而和已经合成的树的关系只有 不组成环 而已

void kruskal(vector<Edge>& edges, int V) {

    //sort函数传递了两个迭代器 和一个回调函数 把edges中的边按权重升序排序

    sort(edges.begin(), edges.end(), compareEdges); // 按权重升序排序

  

    UnionFind uf(V); // 创建并查集

  

    cout << "Edges in the Minimum Spanning Tree:" << endl;

    for (const Edge& edge : edges) {

        int src = edge.src;

        int dest = edge.dest;

        int srcRoot = uf.find(src);

        int destRoot = uf.find(dest);

  

        if (srcRoot != destRoot) { // 如果加入该边不会形成环路

            cout << src << " - " << dest << " (" << edge.weight << ")" << endl;

            uf.unionSets(srcRoot, destRoot);

        }

    }

}

  

int main() {

    int V = 4; // 图中顶点的数量

    vector<Edge> edges = {

        {0, 1, 10},

        {0, 2, 6},

        {0, 3, 5},

        {1, 3, 15},

        {2, 3, 4}

    };

    edges.push_back({1, 2, 1});

    kruskal(edges, V);

  

    return 0;

}
```