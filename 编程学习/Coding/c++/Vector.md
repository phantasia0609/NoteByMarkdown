C++标准库中的`vector`是一个动态数组容器，提供了多种操作和方法来处理动态数组。以下是`vector`中常见的一些操作：

1. **插入操作**：
   - `push_back(val)`: 在容器的末尾插入一个元素。
   - `insert(iter, val)`: 在指定迭代器位置插入一个元素。
   - `insert(iter, n, val)`: 在指定迭代器位置插入n个相同的元素。
   - `insert(iter, begin, end)`: 在指定迭代器位置插入另一个迭代器范围内的元素。

2. **删除操作**：
   - `pop_back()`: 删除容器的最后一个元素。
   - `erase(iter)`: 删除指定迭代器位置的元素。
   - `erase(begin, end)`: 删除指定迭代器范围内的元素。
   - `clear()`: 删除容器中的所有元素。

3. **访问元素**：
   - `at(index)`: 返回指定索引位置的元素，会检查索引是否越界。
   - `operator[](index)`: 通过索引访问元素，不会进行越界检查。
   - `front()`: 返回第一个元素。
   - `back()`: 返回最后一个元素。

4. **容量操作**：
   - `size()`: 返回容器中元素的数量。
   - `capacity()`: 返回容器内存容量，即可以容纳的元素数量。
   - `empty()`: 检查容器是否为空。
   - `reserve(n)`: 分配至少能容纳n个元素的内存空间，可以减少重新分配的次数。

5. **修改容器大小**：
   - `resize(n)`: 改变容器的大小为n，删除或添加元素以适应新的大小。
   - `resize(n, val)`: 改变容器的大小为n，并用val填充新添加的元素。

6. **其他操作**：
   - `swap(vec)`: 交换两个容器的内容。
   - `assign(iter1, iter2)`: 用指定范围内的元素替换容器的内容。
   - `assign(n, val)`: 用n个相同的元素替换容器的内容。

7. **迭代器操作**：
   - `begin()`: 返回指向第一个元素的迭代器。
   - `end()`: 返回指向尾部的迭代器。
   - `rbegin()`: 返回指向反向第一个元素的迭代器。
   - `rend()`: 返回指向反向尾部的迭代器。

这些是`vector`中一些常见的操作，使得它成为一个功能强大且灵活的容器，适用于多种场景，包括动态数组的存储和管理。你可以根据需要选择适当的操作来处理`vector`中的数据。

```c++
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec1 = {1, 2, 3};
    std::vector<int> vec2 = {4, 5, 6};

    std::cout << "Before swap:" << std::endl;
    for (const int &x : vec1) {
        std::cout << x << " ";
    }
    std::cout << std::endl;

    for (const int &x : vec2) {
        std::cout << x << " ";
    }
    std::cout << std::endl;

    std::swap(vec1, vec2); // 使用 std::swap 交换两个容器的内容

    std::cout << "After swap:" << std::endl;
    for (const int &x : vec1) {
        std::cout << x << " ";
    }
    std::cout << std::endl;

    for (const int &x : vec2) {
        std::cout << x << " ";
    }
    std::cout << std::endl;

    return 0;
}

```

```c++
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 使用迭代器进行遍历
    std::cout << "Using iterators to traverse the vector:" << std::endl;
    for (std::vector<int>::iterator it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用 const_iterator 进行遍历（常量迭代器，用于不修改元素的情况）
    std::cout << "Using const iterators to traverse the vector:" << std::endl;
    for (std::vector<int>::const_iterator it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用 auto 关键字进行遍历（C++11 及以后的标准）
    std::cout << "Using auto keyword to traverse the vector:" << std::endl;
    for (auto it = vec.begin(); it != vec.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用范围-based for 循环遍历（C++11 及以后的标准）
    std::cout << "Using range-based for loop to traverse the vector:" << std::endl;
    for (const int &x : vec) {
        std::cout << x << " ";
    }
    std::cout << std::endl;

    return 0;
}

```


# Unique —— Vector 数组排序去重
- vector 的 unique 方法必须在已被 sort 的数组中才可以执行
- 并且 unique 会返回一个迭代器（类似于一个下标）![image.png](https://iili.io/J1QnKfs.png)
- 再调用 erase 方法删除迭代器到 vector 的 end 位置的迭代器的元素（删除）完成目标

