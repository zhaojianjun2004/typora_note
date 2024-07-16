

| 方法                | 类型       | 抽线方法                   |
| ------------------- | ---------- | -------------------------- |
| BiConsumer<T,U>     | 消费型接口 | void accept(T t,U u);      |
| BiFunction<T,U,R>   | 函数型接口 | R apply(T t,U u);          |
| UnaryOperator<T>    | 函数型接口 | T apply(T t);              |
| BinaryOperator<T>   | 函数型接口 | T apply(T t,T t1);         |
| ToIntFunction<T>    | 函数型接口 | int applyAsInt(T t);       |
| ToDoubleFunction<T> | 函数型接口 | double applyAsDouble(T t); |
| IntFunction<R>      | 函数型接口 | R apply(int i);            |
| DoubleFunction<R>   | 函数型接口 | R apply(double d);         |

## day15

#### 一.lambda表达式引出



<!--补充-->

> 1.当有两个实现类实现同一个接口的方法(doFilter)，这个时候如果想返回对应的方法，需要在测试类里面添加一个方法：
>
> ```java
> public static list<Hero> filterHero(list<Hero>list,FilterHero filterHero){
>     return filterHero.doFilter(list);
> }//这里面的filterHero就是相应的实现类的
> ```
>
> 已知有一个实现类FilterHeroByBlood,（接口FilterHero的子类），当我在测试类里面想调用方法传入一个列对象的时候，可以直接使用以下格式
>
> ```java
> //策略模式
> List<Hero>heroes=filterHero(list,new FilterHeroByBlood());
> //这里的参数传入技巧就是使用的java多态向上转型，`父类 对象名= new 子类类型（）`
> 
> ```

>2.匿名内部类的实现：
>
>匿名内部类可以实现接口，并且在内部重写方法，这可以在不创建新类的情况下，直接为接口提供实现
>
>```java
>//匿名内部类的格式
>new 接口名（）{
>    //在这里重写接口方法
>}
>```
>
>



------

#### 二.lambda简介

lambda表达式时java8中一个重要的特性，允许通过表达式来代替功能接口。

lambda可以看作一个匿名内部类的语法糖，也可以成为闭包

- 方便函数式编程
- 代码简洁，开发迅速
- 过滤和计算非常容易
- 改善了集合类的操作



缺点：

- 非并行计算中，未必有传统的for循环性能高
- 不易调试，可读性差



------

#### 三.lambda语法

`parameters->expresion`

`(parameters)->{statements;}`

parameters：类似于方法的参数列表，这里的参数是接口里的参数，可以声明也可以不声明

方法体：可以是表达式也可以是代码块，代码块可以选择性返回值，代码块等于<span style="color:red;">对接口实现</span>的方法体；



------

#### 四.函数式接口

定义：一个接口有且仅有一个抽象方法

lambda表达式允许直接以内联的方式为这种接口创建实例，而不需要显式的编写匿名类



------

#### 五.lambda使用

这里的`MyInter`都是接口，`MyInter2<T>`是泛型接口

- 无参、无返回值

```java
MyInter inter=()->System.out.printLn("hello");
```



- 有一个参数、没有返回值

```java
MyInter2<String>inter2=x->System.out.prinln(x);
```



- 有一个参数有返回值、只有一行语句：右侧大括号和return同时省略

```java
MyInter3 inter3=x->Math.abs(x);
```



- 有两个或以上参数、有返回值

```java
MyInter4 inter4=(x,y)->{
    int sum=1;
    for(int i=1;i<=y;i++){
        sum*=x;
    }
    return sum;
};
System.out.println(inter4.pow(5,3));

interface MyInter4{
    int pow(int x,int y);
}
```



------

#### 六.jkd内置四个核心函数式接口

| 接口名        | 类型                                                         | 抽象方法           |
| ------------- | ------------------------------------------------------------ | ------------------ |
| Consumer<T>   | 消费型接口（）                                               | void accept(T t);  |
| Suppliere<T>  | 供给型接口（可以生产一个需要的数据，又不需要提供参数）       | T get();           |
| Function<T,R> | 函数型接口（需要在一个方法中传入参数，获取一个返回值）       | R apply(T t);      |
| Predicate<T>  | 断言型接口（方法中传入一个参数，方法进行判断，返回boolean类型的值） | boolean test(T t); |



其他接口名：





------

#### 七.方法引用

如果lambda表达式体中的功能有方法实现了，则可以使用方法引用

lambda表达式体中调用方法的参数列表和返回值类型，要和函数式接口中定义的抽象方法参数列表和返回值一致

###### 语法格式：

- 静态方法：`类名::静态方法名`

- 实例方法：`实例对象名::实例方法名`

```java
list.fotEach(System.out::println);//遍历列表
```

- 特殊方法：`类名:实例方法名`
- 构造方法：`类名::new`

```java
BiFunction<String,Integer,Teacher>function=Teacher::new;
System.out.println(function.apply("李白",20));
```

- 数组引用：`数组类型[]::new`

```java
Function<Integer,Integer[]>function=Integer[]::new;
Integer[]apply=function.apply(10);
Arrays.fill(apply,10);
System.out.println(Arrays.toString(apply));
```

- this和super引用：`this::方法名`

  ​								`super::方法名`