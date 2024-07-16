## day21

### 一.Stream流

1.本质上是对集合对象功能的增加，用来处理各自方便高效的操作‘

​	就想工人在流水线上加工一样。只需要告诉需求，流程在后面自行处理，我们只需要得到结果



##### 2.Stream流的作用：

​	结合了Lambda表达式，简化了集合，数组的操作

###### 	使用步骤：

(1)先得到一条Stream流（流水线），并把数据放上去

- <span style="color:red;">单列集合</span> `default Stream<E>stream()`      											使用Collection中的默认方法

```java
List<String>list=new ArrayList<>();
Collections.addAll(list,"a","b");
//获取流水线并将集合的数据打印
list.stream().forEach(s->System.out.println(s));
```



- <span style="color:red;">双列集合</span>  无                                                        										无法直接使用Stream流(keySet()或者entrySet())

```java
HashMap<String,Integer> hm=new HashMap<>();
hm.put("aa",11);
hm.put("bb",22);

//获取Stream流的两种方式
hm.keySet().stream().forEach(s->System.out.println(s));//第一种

hm.entrySet().stream().forEach(s->System.out.println(s));//第二种
```



- <span style="color:red;">数组</span>        `public static <T>Stream<T> stream(T[] array)`          Arrays工具类的静态方法

```java
int []arr={1,3,4,5,6};
String[]arr1={"a","n","m"};

//获取stream流
Arrays.stream(arr).forEach(s->System.out.println(s));
Arrays.stream(arr1).forEach(s->System.out.println(s));
```



- <span style="color:red;"> 一堆零散数据</span> `public static<T> Stream<T> of(T...values)`	   Stream接口中的静态方法

```java
Stream.of(1,2,3,"a").forEach(s->System.println(s));
```



<!--注-->

> Stream接口中静态方法of的细节：
>
> 方法的形参是一个<span style="color:green;">可变参数</span>，可以传递一堆零散的数据，也可以传递数组
>
> 数组必须是<span style="color:green;">引用类型的</span>，如果传递基本数据类型，就会把整个数组当成一个元素，放到stream当中



(2)利用Stream流中的API进行各种操作

> （1）使用<span style="color:red;">中间方法</span>（方法调用之后还可以调用其他方法：过滤filter、转换）
>
> （2）使用<span style="color:red;">终结方法</span>（最后一步，调用完毕之后不能调用其他方法：统计、打印）



#### 3.过滤、切片、聚合

*过滤和切片属于中间操作*

###### （1）过滤：

将符合条件的元素提取出来，到一个新的流中的操作

```java
//例子是将一个list集合中的名字中第一个字是“张”的数据留下
...;
list.stream().filter(s->s.startWith("张")).forEach(System.out::println);
```

##### 注：

> 1.中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程（如上面的代码示例）；
>
> 2.修改Stream流中的数据，<span style="color:red;">不会影响</span>原来的集合或数组的数据



###### （2）切片：

从集合中取出一部分相应的元素重新组成一个集合

- 截断:`limit(long maxSize)`截断流，最大长度不能超过maxSize
- 跳过指定元素：`skip(long n)`,跳过前面元素，从第n个元素开始获取
- 去重：`distinct()`



*聚合是终极操作*

- 取最大值：`max(new Comparator<T>)`
- 取最小值：`min(new Comparator<T>)`
- 统计个数：`count()`



#### 4.一些常用操作：

| 操作      | 说明                                   |
| --------- | -------------------------------------- |
| forEach   | 遍历                                   |
| findFirst | 查找第一个数据，返回Optional           |
| findAny   | 查找任意元素                           |
| anyMatch  | 只要有一个元素符合判断条件，就返回true |
| noneMatch | 每个元素都不符合，返回true             |
| allMatch  | 每个元素都符合，返回true               |

###### findAny：

查找任何元素，返回Optional，

如果是stream，就返回第一个元素，相当于findFirst

如果使用parallelStream，返回随机一个元素





#### 5.Optional类

jdk8引入的新容器类

可以为null，有效的解决了NullPointerExecption的问题

Optional类可以仿有对象，也可以为空；

###### 常用方法：

| 方法                | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| empty()             | 创建一个空的Optional                                         |
| of(T t)             | 创建一个Optional，存储T对象，非空值，如果元素为空，报空指针异常，<span style="color:red;">明确对象不为空</span>使用of()方法 |
| ofNullable(T t)     | 可以有空值，如果为元素为空，报NoSuchElementException异常，<span style="color:red;">不确定对象是否为null</span>，使用ofNullable()方法 |
| get()               | 获取Optional中的value值                                      |
| isPresent()         | 判断值是否存在，存在返会true                                 |
| isEmpty()           | 判断值是否不存在，不存在返回true                             |
| orElse(T t)         | 如果值不为空，则返回值，否则返回false                        |
| orElseGet(Supplier) | 如果为空，执行Supplier接口，并将返回指向结果                 |

