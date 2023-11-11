逻辑设计

数据结构

1. Graph 结构体：图的邻接矩阵表示。主要包括：
   - vertices：顶点数
   - matrix：邻接矩阵
   - path：用于记录中转点的矩阵

2. Edge 结构体：用于邻接表表示的图的边定义，包括：
   - to：到达的顶点编号
   - `weight`：边的权重

调用关系

1. `main()` 函数是程序的入口点。
2. 在 `main` 中首先通过 `readGraphFromFile()` 从文件中读取图的数据。
3. 使用 `Floyd()` 函数计算图中所有顶点对的最短路径。
4. 使用 `findShortestPath()` 函数找到指定起点和终点的最短路径。
5. 用邻接表表示法，然后调用 `dijkstra()` 函数计算单源最短路径。

核心算法

1. **Floyd-Warshall 算法**：用于找到图中所有顶点对的最短路径。
2. **Dijkstra 算法**：用于找到从单个源点到其他所有顶点的最短路径。

物理设计

文件结构

- 从文件 "graph.txt" 中读取图的数据。

输入输出

- 输入：从 "graph.txt" 文件中读取图的数据。
- 输出：打印出 Floyd-Warshall 计算得到的最短路径矩阵和路径矩阵，以及 Dijkstra 算法得到的结果。

#### 存储

- 使用 `matrix` 数组存储图的邻接矩阵。
- 使用 `dist` 和 `path` 二维向量存储 Floyd-Warshall 算法的结果。
- 使用 `adjList` 向量存储图的邻接表表示。

#### 主要函数

- `initGraph()`：初始化图。
- `addEdge()`：将边添加到图中。
- `printFloydMatrix()` 和 `printPathMatrix()`：分别打印 Floyd-Warshall 计算得到的最短路径长度矩阵和路径矩阵。
- `Floyd()`：实现 Floyd-Warshall 算法。
- `readGraphFromFile()`：从文件中读取图的数据。
- `findShortestPath()`：通过 path 矩阵查找从源顶点到目标顶点的最短路径。
- `initGraph2()` 和 `addEdge2()`：与上面的函数类似，但是用于邻接表表示的图。
- `dijkstra()`：实现 Dijkstra 算法。
- `printList()`：打印图的邻接表表示。

为了方便理解，你可以为上述函数绘制流程图或伪代码。