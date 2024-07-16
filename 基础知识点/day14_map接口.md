### day14

#### 一.Map:

##### 1.`Map`接口：

存储的是键值对的对象组

不是Collection接口的子接口，本身是一个顶级的接口

- <span style="color:red;">Map的键和值都必须是引用类型</span>（包装类型），而不能使用基本数据类型，因为Map是一个<span style="color:red;">泛型容器</span>，需要使用对象而不是基本数据类型

容器的元素都是引用数据类型，而数组的元素可以是引用数据类型和基本数据类型



##### 2.`HashMap`

采用hash算法存储数据，<span style="color:red;">Key不能重复，value可以重复</span>

特性：*“无序性、key唯一性、value不唯一性”*

重复的key会对之前的value值进行重写

-  常用方法：

`put(key,value)`向HashMap中存入数据

`get(key)`通过指定的key，获取对应的value

| 方法                                    | 说明                                             |
| --------------------------------------- | ------------------------------------------------ |
| containsKey(key)  /containsValue(value) | 判断Map中是否包含指定的键（值），返回boolean类型 |
| remove(key[,value])                     | 按指定key将元素从Map中移除                       |
| size()                                  | 获取有效元素的个数                               |
| isEmpty()                               | 判断是否为空                                     |
| putAll(map)                             | 将一个指定Map集合加入到当前Map中                 |
| replace(key,value)                      | 将指定的key以给的value进行替换处理               |



##### 3.`LinkedHashMap`

继承自HashMap,有顺序

特性：*有序性、key唯一性、value不唯一性*

##### 4.`TreeMap`

底层采用树结构，不管怎么放入，都<span style="color:red;">按照key默认升序</span>



<!--LinkedHashMap和TreeMap的选择-->

> - LinkedHashMap：保持插入顺序，插入和查找相对快速，有序性要求较低
> - TreeMap：按照键排序，插入和查找相对较慢，有序性要求较高



##### 5.`Hashtable`

- 和`HashMap`均实现Map接口
- HashMap继承了AbstractMap，Hashtable继承了Dictionary抽象类
- Hashtable是线程安全，HashMap非线程安全，HashMap的性能高于Hashtable，我们平时一般使用HashMap
- 



##### 6.`Properties`

继承自`Hashtable`，处理属性文件



------

#### 二,Stack栈：

继承自`Vector`

常见方法：

| 方法                | 说明                                           |
| ------------------- | ---------------------------------------------- |
| push(E)             | 压栈（进栈）操作                               |
| pop()               | 栈顶获取一个元素并移除                         |
| peek()              | 栈顶获取一个元素“不”移除                       |
| empty()  /isEmpty() | 判断栈使用为空                                 |
| search(Object)      | 查找一个元素在栈中的位置，如果没有找到就返回-1 |



------

#### 三.递归：

方法自己调用自己



------

#### 四.队列：

队首（Front）:允许删除的一端

队尾（Rear)：允许插入的一端

分类：1.按方向：单向、双向

​			2.按阻塞情况：阻塞队列、非阻塞队列

​			3.按是否有界：有界、无界



##### 1.Queue:

是一个接口，单向队列，继承自Collection

除了基本的集合接口操作，还提供了特殊的插入、获取、移除的操作

|      | 抛出异常的方法 | 返回null和false的方法 |
| ---- | -------------- | --------------------- |
| 插入 | add(e)         | offer(e)              |
| 移除 | remove()       | poll()                |
| 获取 | element()      | peek()                |



##### 2.Deque:

是一个接口，双向队列，继承自Queue

特点：先进先出、后进先出

