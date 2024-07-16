### day13

#### 一.链表

非连续，非顺序的存储结构

数据元素之间的逻辑顺序是通过链表中的<span style="color:red;">指针链接次序</span>实现的

链表由<span style="color:red;">一系列结点</span>>组成，结点可以<span style="color:red;">运行时动态</span>生成

##### 1.分类：

###### 单向链表：

###### 双向链表：

###### 循环链表：



#### 二.自定义链表

- 有效元素个数：`private int size;`
- 头结点：`private Node<E> first;`
- 尾结点：`private Node<E> last;`

结点类的创建：

```java
private class Node<E> {
    Node <E> next;//指向后继结点
    E data;//数据元素
    Node<E> previous;//指向前驱结点
    
    //构造函数
    public Node(Node<E> next,E data,Node<E> previous){
        this.next=next;
        this.data=data;
        this.previous=previous;
    }
}
```



#### 三.LinkedList

底层使用链表数据结构:

> `LinkedList`类基于链表的结点结构实现，通过维护一个指向链表头部和尾部的引用来支持<span style="color:red;">高效的插入和删除操作</span>，在底层实现中，`LinkedList`会通过结点之间的引用关系来连接链表的各个结点

###### 新增方法：

| 方法                                 | 说明                                           |
| ------------------------------------ | ---------------------------------------------- |
| addFirst(Object)    /addLast(Object) | 将给定元素插入链表的开头/ 结尾                 |
| getFirst()   /getLast()              | 获取链表的头结点元素值   /尾结点               |
| removeFirst()   /removeLast()        | 移除链表的头结点（尾结点），并返回其中的元素值 |



#### 四.`ArrayList`和`LinkedList`比较：

##### 1.存储结构：

`ArrayList`:底层是数组结构，<span style="color:red;">线性顺序存储</span>

`LinkedList`底层是链表结构，<span style="color:red;">非连续、非顺序</span>的存储。 

​					对象间是依靠<span style="color:red;">指针域</span>连接起来

##### 2.操作性能：

`ArrayList`适合随机查询数据

`LinkedList`适合元素的动态插入和删除



#### 五.Vector向量：

和ArrayList处理方式底层一样都是<span style="color:red;">数组结构</span>



#### 六.哈希表：

散列表（哈希表），通过<span style="color:red;">键和值</span>直接进行访问的数据结构

存放记录的数组就是哈希表

使用元素的存储位置和它的键值建立一个映射关系，加快查找速度





#### 七.HashSet:

底层使用`HashMap`,将数据存储到HashMap的key上面

<span style="color:red;">无序性、唯一性</span>



#### 八.LinkedHashSet:

<span style="color:red;">是HashSet的子类</span>

底层是一个LinkedHashMap，维护了一个数组+双向链表

根据元素的HashCode值来决定元素的存储位置，同时使用链表维护元素的次序，使用元素看起来是以插入顺序保存的

特点·：<span style="color:red;">有序性、唯一性</span>



#### 九.TreeSet:

底层数据结构是二叉树

使用TreeSet时候，要求存储的元素具有<span style="color:red;">可比较性</span>

根据二叉树算法将数据排列，使用<span style="color:red;">中序遍历</span>，读出来的元素顺序都是<span style="color:red;">升序排列</span>

TreeSet泛型的对象，需要具有能力排序（Comparable），如果没有实现Comparable接口，则需要在TreeSet构造方法中传入Comparator接口的对象





#### 十.排序接口：

做对象的排序时，使用两种方式：

`Compareable接口`：

`Comparator接口`：



#### 十一.Collections工具类：（集合工具类）

| 方法                                                    | 说明                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| <span style="color:red;">sort(list[,Comparator])</span> | 按升序排列（按外部比较器规则排序）                           |
| <span style="color:red;">reverse(list)</span>           | 按降序排列                                                   |
| <span style="color:red;">shuffle(list)</span>           | 随机排序                                                     |
| swap(list,int,int)                                      | 交换两个索引位置的元素                                       |
| max(list)  /min(list)                                   | 获取集合中的最大值(最小值)                                   |
| binarySearch(list,object)                               | 二分查找，返回索引                                           |
| replaceAll(list,Object,Object)                          | 将list集合中的旧元素换成新元素                               |
| frequentcy(collection,Object)                           | 统计元素出现的次数                                           |
| rotate(list,int)                                        | 旋转，如果第二个参数为0，就没有改变，如果为整数，就将list集合最后几位移动到集合前面，如果为负数，就将list集合前几位元素移动到后面 |



<!--知识点区分-->

##### Array数组类与Arrays工具类；

​	Array类是Java中<span style="color:red;">最基本的有关存储结构</span>，

Arrays类是java中<span style="color:red;">提供的一个工具类</span>,在java.util包中，包含一些方法用来直接操作数组，比如如何实现数组的排序、搜索等，



##### Collection接口与Collections工具类：

集合接口Collection是java.util包下<span style="color:red;">集合类的上级接口</span>，继承与它有关的接口主要有List和Set;

Collections工具类是<span style="color:red;">针对集合类的有关静态工具类</span>，它包括有关集合操作的静态方法，它提供一些列静态方法实现对各种集合的搜索、排序、线程安全等操作；

