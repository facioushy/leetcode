# 集合篇

## 1. Vector、ArrayList、LinkedList区别，分别适合在什么场景

#### Vector

是 Java 早期`提供的线程安全的动态数组`，如果不需要线程安全，**并不建议选择**，毕竟同步是有额外开销的。Vector 内部是使用对象数组来保存数据，可以根据需要自动的增加容量。当数组已满，开始扩容时，会先创建新的扩容后数组，并拷贝原有数组数据，最后删除原数组。

#### ArrayList：

适合“查询”和“更新“场景。

随机查询效率：（优势），ArrayList 比 LinkedList 在随机访问的时候效率要高，因为 `LinkedList 是线性的数据存储方式，所以需要移动指针从前往后依次查找`，而ArrayList根据角标index直接锁定位置。

插入和删除效率：在List中间插入和删除数据时，ArrayList 要比 LinkedList 效率低很多，因为 ArrayList 增删操作要影响数组内的其他数据的下标（整体移动），而如果是正常的末尾追加方式，效率大体相同。 内存空间占用：LinkedList 比 ArrayList 更占内存，因为 LinkedList 的节点除了存储数据，还存储了两个引用，一个指向前一个元素，一个指向后一个元素。

#### LinkedList

适合”插入“和”删除“场景

数据结构:LinkedList 是双向链表的数据结构实现。 随机查询效率：相比ArrayList （劣势） 插入和删除效率：LinkedList按序号查询数据时需要进行前向或后向遍历，但插入数据时只需要记录当前项的前后项即可，增删时也只需修改链表指向即可，所以 LinkedList 插入和删除速度较快。（优势） 内存空间占用：相比ArrayList （劣势）

### 多线程场景下不能使用ArrayList吗？

我们知道ArrayList 不是线程安全的，如果遇到多线程场景，可以通过 Collections 的 synchronizedList 方法将其转换成线程安全的容器后再使用。例如像下面这样：

```java
List<String> syncList = Collections.synchronizedList(arraylist);
```

## List和Set区别

* **重复对象**

list方法可以允许重复的对象，而set方法不允许重复对象；

* **null元素**

list可以插入多个null元素，而set只允许插入一个null元素；

* **容器是否有序**

list是一个有序的容器，保持了每个元素的插入顺序。即输出顺序就是输入顺序，而set方法是无序容器，无法保证每个元素的存储顺序，TreeSet通过 Comparator 或者 Comparable 维护了一个排序顺序。

* 常用的实现类 list方法常用的实现类有：

  ArrayList、LinkedList 和 Vector。ArrayList最常用，提供使用索引（index）访问，定位、查询效率高；而LinkedList 则对于经常需要从 List 中添加或删除元素的场合更为合适，Vector 表示底层数组，线程安全，效率低被边缘化~

  Set方法中常用的实现类有:

  HashSet、LinkedHashSet 以及 TreeSet。最常用的是基于 HashMap 实现的 HashSet；另外TreeSet 还实现了 SortedSet 接口（支持排序），因此 TreeSet 是一个可根据 compare\(\) 和compareTo\(\)方法进行排序的有序容器。

* **遍历方式**

List 支持for循环，也就是通过下标来遍历，也可以用迭代器（Iterator），但是set只能用迭代，因为他无序，无法用下标来取得想要的值。

### Set和List效率上对比怎样

`Set`： 删除和插入效率高，插入和删除不会引起元素位置改变。检索元素的话，效率低下；当然，在`理想情况下`，不考虑哈希冲突的情况，且仅需一次定位即可完成，时间复杂度为O\(1\)，但是不现实。

`List`： 和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变

### hashSet实现原理

HashSet 底层是基于 HashMap 实现的，能够继承 HashMap 的所有特性，因此 HashSet 结构也是数组+链表+红黑树，同样也不能使用get方法，HashSet 的操作，基本上都是直接调用底层 HashMap 的相关方法来完成，不允许key重复，但支持null对象作为key。

### HashSet如何保证key不重复

当我们对一个HashSet 的实例添加一个值时，使用到的是它的 add 方法，其底层维护了一个HashMap来实现元素的添加。我们知道，HashMap 作为双列集合，它的键是不能够重复的，`HashMap 针对 hashCode 相同且 equals 比较值相同的时候执行的是更新操作`，所以Hashmap中的key是唯一的，也决定了hashset元素值也是唯一的。

## Array和ArrayList区别

Array 可以存储基本数据类型和对象，ArrayList 只能存储对象。 Array 是指定固定大小的，而 ArrayList 大小是自动扩展的。 Array 内置方法没有 ArrayList 多，比如 addAll、removeAll、iteration 等方法只有 ArrayList 有。

Array 和 ArrayList可以互相转换，Array 转 List有： Arrays.asList\(array\)；而List 转 Array有：List.toArray\(\)方法。

