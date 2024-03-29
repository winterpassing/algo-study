1.数组（Array）是一种线性表数据结构。它用一组连续的内存空间，来存储一组具有相同类型的数据。

线性表（Linear List）。顾名思义，线性表就是数据排成像一条线一样的结构。
每个线性表上的数据最多只有前和后两个方向。除了数组，链表、队列、栈也是线性表结构。
二叉树、堆、图等为非线性表。数据之间并不是简单的前后关系。

连续的内存空间和相同类型的数据。正式因为这两个限制，它才有了"随机访问"
的特性。有利有弊，插入和删除变得低效，因为要保证内存连续性。

2.计算机会给每个内存单元分配一个地址，计算机通过地址来访问内存中的数据。
当计算机需要访问数组中的某个元素时，它会首先通过下面的寻址公式，计算出该元素的内存地址：
    
`a[i]_address = base_address + i * data_type_size`

data_type_size表示数组中每个元素的大小。根据下标随机访问的时间复杂度为O(1)。

3.低效的插入和删除有哪些改进方法。

如果在数组的末尾插入元素，那就不需要移动数据了，时间复杂度为O(1)。但如果
在数组的开头插入元素，那所有的数据都需要依次往后移动一位，所以最坏时间复杂度是O(n)。
因为我们在每个位置插入元素的概率是一样的，所以平均情况复杂度为(1+2+...+n)/n=O(n)。

如果数组中的数据是有序的，我们在某个位置插入一个新的元素时，就必须按刚才的方法搬移k之后的数据。
但是，如果数组中存储的数据并没有规律，数组只是被当作一个存储数据的集合。在这种情况下，如果
要将某个数据插入到第k个位置，为了避免大规模的数据搬移，可以之间将第k位的数据搬移到数组元素的最后，
把新的元素直接放入第k个位置。利用这种处理技巧，在特定场景下，时间复杂度就会降为O(1)。

删除操作也类似，可以先记录下已经删除的数据，当数组没有更多空间存储数据时，我们再触发一次真正的删除操作。
这就大大减少了删除操作导致的数据搬移。

4.容器是否完全替换数组？

ArrayList最大的优势就是可以将很多数组操作的细节封装起来。比如数组的插入、删除数据时需要搬移其他数据等。
另外，它还有一个优势，就是支持动态扩容。

数组本身在定义的时候需要预先指定大小，因为需要分配连续的内存空间。如果我们申请了大小为10的数组，
当第11个数据需要存储到数组中时，我们就需要重新分配一块更大空间，将原来的数据复制过去，然后再将新的数据插入。

如果使用ArrayList，我们就完全不需要关心底层的扩容逻辑，ArrayList已经帮我们实现好了，每次存储空间不够的时候，
它都会将看空间自动扩容为1.5倍的大小。

因为扩容操作涉及内存申请和数据搬移，是比较耗时的。所以，如果事先能确定需要存储的数据大小，最好在创建的时候事先
指定大小。

* Java ArrayList无法存储基本类型，比如int、log，需要封装为Integer、Long类，而Autoboxing、Unboxing
则有一定的性能消耗，所以如果特别关注性能，或者希望使用基本类型，就可以选用数组。

* 如果数据大小事先已知，并且对数据的操作非常简单，用不到ArrayList提供的大部分方法，也可以直接使用数组。

对于业务开发，直接使用容器就足够了，省时省力。损耗一丢丢性能，完全不会影响系统整体的性能。但如果是底层开发，
比如开发网络框架，性能的优化需要做到极致，这个时候数组就会优于容器，成为首选。



