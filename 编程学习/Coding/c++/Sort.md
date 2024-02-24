Sort 关键字的排序是左闭右开的

在 C++中，`sort` 并不是一个关键字，而是标准模板库（Standard Template Library, STL）中的一个函数，用于对序列进行排序。这个函数定义在头文件 `<algorithm>` 中。`std::sort` 可以对数组、向量（`std::vector`）、或者任意通过迭代器定义的序列进行排序。

### 基本用法

`std::sort` 的最基本用法需要两个迭代器作为参数，分别指向要排序的序列的开始和结束：

```cpp
#include <algorithm> // 包含sort函数
#include <vector>

std::vector<int> vec = {4, 1, 3, 2};
std::sort(vec.begin(), vec.end());
```

上面的代码将 `vec` 中的元素进行升序排序。

### 自定义比较函数

`std::sort` 也可以接受第三个参数，这是一个比较函数，用于自定义排序准则。这个比较函数必须能够接受序列中的两个元素作为参数，并返回一个布尔值，指示第一个参数是否应该排在第二个参数之前。

```cpp
#include <algorithm>
#include <vector>

bool compare(int a, int b) {
    return a > b; // 降序
}

std::vector<int> vec = {4, 1, 3, 2};
std::sort(vec.begin(), vec.end(), compare);
```

或者使用 Lambda 表达式简化：

```cpp
std::sort(vec.begin(), vec.end(), [](int a, int b) {
    return a > b; // 降序
});
```

### 时间复杂度

`std::sort` 的平均时间复杂度是 O(NlogN)，其中 N 是序列的长度。这是因为 `std::sort` 通常实现为快速排序、堆排序或其他 O(NlogN)复杂度的排序算法的混合体，具体实现依赖于编译器和标准库的实现。

### 注意事项

- `std::sort` 默认进行升序排序，除非通过自定义比较函数指定了不同的排序准则。
- 自定义比较函数必须确保排序的“严格弱序”，即比较函数对于两个不同的元素不能同时返回 `true`。
- 对于非随机访问迭代器（如 `std::list` 的迭代器），`std::sort` 不能直接使用，因为 `std::sort` 需要随机访问迭代器。对于这些容器，它们通常提供了自己的 `sort` 成员函数。

通过这种方式，`std::sort` 为 C++程序员提供了一个强大且灵活的排序工具，可以轻松地对数据进行排序操作。