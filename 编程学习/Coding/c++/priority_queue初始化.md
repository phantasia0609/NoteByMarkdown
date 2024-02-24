# 默认类型
在 C++中，可以通过使用标准库中的 `std::priority_queue` 来定义最小堆和最大堆。`std::priority_queue` 默认是一个最大堆，但可以通过传递自定义比较函数来改变其行为，实现最小堆。

### 定义最大堆

最大堆可以直接使用 `std::priority_queue` 的默认行为，不需要任何修改。在最大堆中，顶部元素（通过 `top()` 访问）是队列中最大的元素。这里是一个最大堆的基本用法示例：

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> maxHeap;

    // 添加元素
    maxHeap.push(10);
    maxHeap.push(30);
    maxHeap.push(20);

    // 打印并移除顶部元素
    std::cout << maxHeap.top() << std::endl; // 输出: 30
    maxHeap.pop();

    // 新的顶部元素
    std::cout << maxHeap.top() << std::endl; // 输出: 20

    return 0;
}
```

### 定义最小堆

最小堆需要使用 `std::priority_queue` 时传递一个自定义的比较函数或对象。`std::greater<T>` 是一个预定义的比较函数，可用于创建最小堆。这里是一个最小堆的基本用法示例：

```cpp
#include <iostream>
#include <queue>
#include <functional>

int main() {
    // 使用 std::greater<T> 来定义最小堆
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;

    // 添加元素
    minHeap.push(10);
    minHeap.push(30);
    minHeap.push(20);

    // 打印并移除顶部元素
    std::cout << minHeap.top() << std::endl; // 输出: 10
    minHeap.pop();

    // 新的顶部元素
    std::cout << minHeap.top() << std::endl; // 输出: 20

    return 0;
}
```

在这两个示例中，`std::priority_queue` 的第二个模板参数是用于存储元素的容器类型，而第三个模板参数是用于比较元素的函数。在最小堆的例子中，通过使用 `std::greater<int>` 作为比较函数，保证了顶部元素是队列中最小的元素。

通过这种方式，`std::priority_queue` 提供了灵活的机制来实现最大堆和最小堆，适用于各种需要快速访问最大或最小元素的场景。

# 自定义类型
使用自定义类型在 C++的优先队列中时，你需要提供一个比较类来定义优先级。比较类是一个重载了 `operator()` 的结构体或类，该操作符接受两个自定义类型的参数，并返回一个布尔值，指示第一个参数是否应该被视为低于第二个参数。这种方式允许优先队列确定元素间的排序。

这里是一个简单的例子，展示如何使用自定义类型和比较类来初始化一个优先队列：

### 定义自定义类型

假设你有一个 `Task` 类，每个 `Task` 都有一个 `priority` 和 `name`：

```cpp
class Task {
public:
    int priority;
    string name;

    Task(int p, string n) : priority(p), name(n) {}
};
```

### 定义比较类

接下来，定义一个比较类来比较两个 `Task` 对象。如果你想让优先级数值较小的任务具有较高的优先级（即创建一个最小堆），你可以这样实现比较类：

```cpp
class CompareTask {
public:
    bool operator()(const Task& t1, const Task& t2) {
        // 返回true如果t1的优先级高于t2
        return t1.priority > t2.priority;
    }
};
```

### 初始化优先队列

有了自定义类型和比较类，你可以这样初始化一个优先队列：

```cpp
std::priority_queue<Task, std::vector<Task>, CompareTask> pq;
```

这行代码创建了一个存储 `Task` 对象的优先队列，其中包含一个 `std::vector<Task>` 作为其底层容器，并使用 `CompareTask` 作为比较逻辑，确保优先队列按照任务的优先级进行排序。

### 使用优先队列

现在你可以向优先队列中添加 `Task` 对象，并保证它们按照优先级排序：

```cpp
pq.push(Task(10, "LowPriority"));
pq.push(Task(1, "HighPriority"));

while (!pq.empty()) {
    Task t = pq.top();
    cout << t.name << " ";
    pq.pop();
}
```

这段代码会首先处理名为"HighPriority"的任务，因为它有更高的优先级（在这个上下文中，更小的 `priority` 值意味着更高的优先级）。

通过这种方式，你可以灵活地定义优先队列中元素的优先级，使其适应各种不同的场景和需求。

## 自定义 cmp 函数
- 下图是 u > v 是一个小根堆
- 如果修改成 u < v 则是一个大根堆
- *这和 sort 方法中的 cmp 函数相反*
``` cpp
struct cmp
{
    bool operator()(const ll &u, const ll &v) const
    {
        return u > v;
    }
};
priority_queue<ll, vector<ll>, cmp> pq;
```