# 第五章 标准库代码阅读（STL容器）

# 分配器

分配器主要是给容器使用的，不建议用户使用

# new和malloc

在c++中不管是new还是stl容器的内存分配在最后都会指向malloc

在vc中提供的stl中，其allocator（分配器）当他需要分配内存的时候，会调用malloc

vc中的alloctor只是以::operator new和::operator delete完成allocator和deallocator，没有其他特殊设计

在GNUc++中aloctor也是调用c语言的maolloc和free，

但其实这样的做法效率很低，开销很大，反而很慢，所以并stl中并没有使用该文件

# 深度探索list

list上容器里面最具代表性的，list是一个双向环状链表

指针的大小在32位电脑上是4

在list中一个节点分为：前指针，后指针，元素

所以，我们在使用list的时候，存储数据，sizeof()并不是只有数据本身，还存在两个指针的大小

刻意在环状list尾端加一个空白节点，用以符合STL“前闭后开”的原则

# 深度探索vector

在内存中，申请多少空间就是多少空间，而vector的空间增长是两倍的增长，他说如何实现的？

在vector中，当现在申请的内存不足的时候，vecor会自动的在另外一块内存申请两倍的空间。

在vector中，vector的初始空间大小是1，不能为0，因为0的两倍还是0

在每次扩充成长空间的时候，会把原来的内存拷贝都新申请的空间，原来的空间会被删除，这个时候会大量的调用拷贝构造函数和析构函数，取决于你的元素大小

# 深度探索array，forward_list

为什么有array，array本质上就上一个数组，但是为了对array对有迭代器，size等容器等操作

array在使用的时候，必须指定类型和大小

array<int,10> ar;

---

在array中，允许你给定的大小为0，但是依旧会给1

array中没有构造函数和析构函数，因为语言中的数组没有构造函数和析构函数

forward_list是一个单项的链表

# 深度探索deque

双向开口的容器，双向进出的容器

stack和queue都不允许遍历，也不提供迭代器

stack和queue都可以选择list或deque作为底层结构

stack可以选择vector作为底层结构，但是queue不能使用vector作为底层结构

stack都不可以使用set和map作为底层结构

# 容器rb_tree(红黑树)

红黑树：是平衡二元搜索树中常用的一种平衡搜索树：排列规则有利search和insert，并保持过度平衡，无任何一个节点过深

红黑树提供遍历和迭代器。

按正常规则遍历，便能获得排序状态

我们不应使用红黑树的迭代器改变元素值（因为元素有其严谨的排列规则）。编程层面并未阻绝此事。如此设计树正确的，因为红黑树即为set和map服务（作为其底部支持），而map允许元素的date被改变，只有元素的key才是不可以被改变的

红黑树提供两种插入操作：insert_unique()和insert_equal()，前者表示节点的key一定在整个tree中树独一无二的否则安插失败，后者表示节点的key可以重复

# 容器set,multiset

set/multiset以rb_tree为底层结构，因此有【元素自动排序】特性。排序的依据是key，而set/multiset元素的value和key合一：value就是key。

set/multiset提供“遍历”操作及iterators。按正常规则（++ite）遍历，便能获取排序状态（sorted）

我们无法使用set/multiset的iterators改变元素值（因为key有严谨排序规则）。set/multiset的iterator是其底部的RB_tree的const-ierator，就是为了禁止用户对元素赋值

set元素的key必须独一无二，因此其insert()用的是rb_tree的insert_unique()

multiset元素的key可以重复，因此其insert()用的是rb_tree的insert_equal()

# 容器map,multimap

map/multimap以rb_tree为底层结构，因此有【元素自动排序】特性。排序的依据是key

map/multimap提供“遍历”操作及iterators.

按正常规则（++ite）遍历，便能获得排序状态

我们无法使用map/multimap的iterators改变元素的key（因为key有其严谨排列规则），但可以用它来改变元素的date，因此map/multimap内部自动将用户指定的key type设为const，如此便能禁止用户对元素的key赋值

map元素的key必须独一无二，因此其insert()用的是rb_tree的insert_unique();

multimap元素的key可以重复，因此其insert()用的是rb_tree的insert_equal();

# 容器hashtable（哈希表）

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055767-1bb2be36-d4c2-4eac-b583-846028acb356.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055767-1bb2be36-d4c2-4eac-b583-846028acb356.png)

---

当空间足够的时候，我们把元素放置到元素的个数的位置上

当空间不够的时候，我们把元素放到元素个数除以空间长度的余数上

【如果发生碰撞怎么办？】

如果发生碰撞，那么就把该位置变成链表

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055750-f9b7f69a-df41-41b1-a239-abaf6c9a442d.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055750-f9b7f69a-df41-41b1-a239-abaf6c9a442d.png)

---

这种做法叫做Separate,Chaining

虽然liat是线性搜索时间，如果list够小，搜索速度仍然很快

# unordered容器（不定序容器）

将原先的哈希散列表更换为了不定序rongq

![https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055744-f5ad7d88-ed14-4dac-9d68-a77eb9ca811b.png](https://cdn.nlark.com/yuque/0/2024/png/23087967/1717314055744-f5ad7d88-ed14-4dac-9d68-a77eb9ca811b.png)

---