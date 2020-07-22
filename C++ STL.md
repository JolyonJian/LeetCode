# C++ STL

记录了解题过程中使用到的STL及其基本用法。

## auto;const auto&

**auto:**在块作用域、命名作用域、循环初始化语句等等 中声明变量时，关键词auto用作类型指定符。

**const:**修饰符

### auto

即 `for(auto x:range) `这样**会拷贝一份`range`元素，而不会改变`range`中元素**；

  但是使用`for(auto x:vector<bool>)`时得到一个`proxy class`,操作时会改变`vector<bool>`本身元素。应用：`for(bool x:vector<bool>)。`

### auto&

当**需要修改range中元素**，用`for(auto& x:range)` 当`vector<bool>`返回临时对象，使用`auto&`会编译错误，临时对象不能绑在`non-const l-value reference `（左值引用）需使用`auto&&`,初始化右值时也可捕获。

### const auto&  

​     当只想读取`range`中元素时，使用`const auto&`,如：`for(const auto&x:range)`,它**不会进行拷贝，也不会修改`range`**。 

### const auto

​    当**需要拷贝元素，但不可修改拷贝出来的值**时，使用 `for(const auto x:range)`，避免拷贝开销 。

***

## [vector](http://www.cplusplus.com/reference/vector/vector/)

### 基本特性

**1. 顺序序列**

顺序容器中的元素按照严格的线性顺序排序。可以通过元素在序列中的位置访问对应的元素。

**2. 动态数组**

支持对序列中的任意元素进行快速直接访问，甚至可以通过指针算述进行该操作。操供了在序列末尾相对快速地添加/删除元素的操作。。

**3. 能够感知内存分配器（Allocator-aware）**

容器使用一个内存分配器对象来动态地处理它的存储需求。

与`array`相比，`vector`消耗更多的内存以换取管理存储和以有效方式动态增长的能力。

与其他动态序列容器（`deques`，`lists`和`forward_lists`）相比，`vector`在访问其元素方面非常有效，并且从其末尾添加或删除元素都相对高效。对于涉及在末尾以外的位置插入或删除元素的操作，它们的性能比其他方法差，并且与`lists`和`forward_lists`相比，迭代器和引用的一致性更差。

### 基本用法

```C++
#include<vector>
using namespace std;
```

### 基本函数实现

* `vector(int nSize,const t& t)`:创建一个vector，元素个数为nSize,且值均为t
* `void push_back(const T& x)`:向量尾部增加一个元素X
* `void pop_back()`:删除向量中最后一个元素
* `iterator erase(iterator it)`:删除向量中迭代器指向元素
* `void clear()`:清空向量中所有元素
* `reference at(int pos)`:返回pos位置元素的引用
* `reference front()`:返回首元素的引用
* `reference back()`:返回尾元素的引用
* `iterator begin()`:返回向量头指针，指向第一个元素
* `iterator end()`:返回向量尾指针，指向向量最后一个元素的下一个位置
* `int size() const`:返回向量中元素的个数
* `bool empty() const`:判断向量是否为空，若为空，则向量中无元素
* `*max_element(vactor.begin(),vector.end())`:返回向量中的最大值
* `*min_element(vactor.begin(),vector.end())`:返回向量中的最小值

***

## [unordered_map](http://www.cplusplus.com/reference/unordered_map/unordered_map/)

### 基本特性

C++ STL中，哈希表对应的容器是 `unordered_map`（since C++ 11）。根据 C++ 11 标准的推荐，用 `unordered_map` 代替 `hash_map`。

哈希表是根据关键码值(key value)而直接进行访问的数据结构。也就是说，它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度，这个映射函数叫做散列函数。

哈希表的一个重要问题就是如何解决映射冲突的问题。常用的有两种：**开放地址法** 和 **链地址法**。

**与 map 的区别：**

STL中，`map` 对应的数据结构是 **红黑树**。红黑树是一种近似于平衡的二叉查找树，里面的数据是有序的。在红黑树上做查找操作的时间复杂度为 `O(logN)`。而 `unordered_map` 对应 **哈希表**，哈希表的特点就是查找效率高，时间复杂度为常数级别 `O(1)`， 而额外空间复杂度则要高出许多。所以对于需要高效率查询的情况，使用 `unordered_map` 容器。而如果对内存大小比较敏感或者数据存储要求有序的话，则可以用 `map` 容器。

### 原型

```C++
template<
  class Key,
  class T,
  class Hash = std::hash<Key>,
  class KeyEqual = std::equal_to<Key>,
  class Allocator = std::allocator<const Key, T> >
> class unordered_map;
```

### 基本用法

```C++
#include <unordered_map>
using namespace std;
```

### 基本函数实现

* `mapped_type& at ( const key_type& k ):`对键值等于*k*的元素的映射值的引用。

* `size_type bucket ( const key_type& k ) const`:返回 Key 值为输入参数 k 的元素的所在桶号。
* `size_type count ( const key_type& k ) const`:如果容器中存在具有该 Key 值的元素，则该函数返回 1，否则返回 0。
* `void clear() noexcept`:清除所有元素；
* `bool empty() const noexcept`:判断向量是否为空，若为空，则向量中无元素
* `size_type erase ( const key_type& k )`:删除指定位置的元素；
* `void insert ( initializer_list<value_type> il )`:在指定位置添加 pair 类型的元素；
* `const_iterator find ( const key_type& k ) const`:获取元素的迭代器；
* `begin, end`:正向迭代器的起始位置与终点位置；

***

