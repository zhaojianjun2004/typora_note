## day22

### 一.映射操作：

属于中间操作

##### 1.map映射操作



2.flatMap映射操作



3.mapToInt mapToLong mapToDouble



### 二.归约reduce：

缩减操作，把一个流缩减成一个值，实现对集合求和、求乘积、求最大值、最小值操作

<span style="color:red;">终端操作</span>，

可操作基本数据类型和引用数据类型

```java
Optional<Integer>reduce=stream.reduce(Integer::min);
System.out.println(reduce.get());
```



### 三.sorted排序操作：

<span style="color:red;">中间操作</span>

sorted():自然排序，要求流中的元素实现Comparable接口

sorted(Comparator comparator)自定义排序



### 四.收集collect：

<span style="color:red;">终端操作</span>

使用以下方法的时候都是`collect(Collectors.)`的形式

把一个流搜集起来，最终可以是收集成一个值，也可以收集成一个新的集合

流不储存数据，所以要放到一个新的集合中，toList、toSet、toMap、toCollection

```java
collect(Collectors.toList());
```

###### 1.统计与计算

counting:统计数量，可以用count替换

maxBy:获取最高值，可以用max替换(可以加Comparator比较器)

```java
list.stream().collect(collectors.minBy(Comparator.comparingInt(Emp::getSal)));
```

minBy:获取最低值，可以用min替换

summingInt:求和，可以用数值流sum替换

averagingDouble:求平均值，可以用数值流average替换

```java
Integer collect=list.stream().collect(Collectors.summingInt(Emp::getSal));
```

summarizingInt:一次性获取所有相关信息，等价于数值流的summaryStatistics



###### 2.分组

`partitioningBy`，只能分成两组，符合和不符合分别为一组

返回结果为Map,Key，Boolean类型，分成true和false

```java
Map<Boolean,List<Emp>>collect=list.stream().collect(Colletors.partitioningBy(x->x.getSal()>=1000));
collect.forEach((k,v)->{
    System.out.println(k);
    v.forEach(System.out::println);
});
```

`groupingBy`将集合分成多个Map，如按照年龄分组，或者按工资

```java
Map<String,List<Emp>listMap=list.stream(),collect(Collectors.groupingBy(e->{
    if(e.getAge()<30)
        return "青年";
    else
        return "中年";
}));
```



###### 3.拼接操作joining

可以将Stream中的元素，按指定的特殊符号拼接，得到一个字符串

三种方式：

- 无参，直接拼接
- 一个参数，连接符号
- 三个参数，连接符，前缀，后缀

```java
String str=list.stream().map(Emp::getName).collect(Collectors.joining("_","|","|"));
System.out.println(str);
```



###### 4.归约reducing

```java
//Optional<Integer>sum=stream.collect(Collectors.reducing(Integer::sum));
Optional<Integer>reduce=stream.reduce(Integer::sum);
System.out.println(reduce.get());
```

