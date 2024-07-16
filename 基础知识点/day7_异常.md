### day7

#### 一.java异常（Exception）

1. RuntimeException:运行时异常：程序运行时抛出，可以通过反复测试尽量避免，不应该靠异常处理机 制来解决。

| 运行时异常                     | 说明                 |
| ------------------------------ | -------------------- |
| ArrayIndexOutOfBoundsException | 数组下标越界异常     |
| NullPointerException           | 访问null对象引用     |
| java.lang.ClassCastException   | 类型转换异常         |
| ArithmeticException            | 算数异常，如除零操作 |

​	2.CheckedException:检查型异常：编译器对代码进行检查，如果没有处理异常，不允许程序通过。

| 检查型异常             | 说明                   |
| ---------------------- | ---------------------- |
| InterruptedException   | 线程中断异常           |
| IOException            | 输入输出流异常         |
| ClassNotFoundException | 类找不到异常           |
| InputMismatchException | 输入数据格式不符合预期 |

​	3.异常体系中最上层父类是Exception（再上层是Throwable），异常分为编译时异常（直接继承于Exception），运行时异常（RuntionException本身和子类）

###### 4.异常的作用：

（1）异常来查询bug的关键参考信息

（2）异常可以作为<span style="color:red;">方法内部</span>的一种特殊返回值



#### 二.异常处理

1.不处理：运行时异常；

##### 	捕获：

```java
try{
    //可能会出现异常，需要接受监视的代码
}catch(异常类型 e){
    //异常发生后，处理预案
}
```

在一个try块中，可能会会出现多个异常。可以接多个catch，去捕捉不同的异常

```java
try{
    
}catch(异常1 e){
    
}catch(异常2 e){
    
}//如果try中出现异常，直接进入对应的catch块中，try中出现异常后的代码不会继续执行
```

jdk7之后可以在一个catch块中捕获多个异常（用 | 分隔）

如果异常没有被捕获，则异常会交给jvm虚拟机处理



异常信息的处理：

- e.getMessage():获取异常信息

- e.toString():获取异常类和信息

- e.printStackTrace():打印异常堆栈轨迹

  ##### 抛出：

  throw、throws关键字

  用法：`throw Throwable类或其子类对象`

throw在方法体内的语句，如果抛出的是<span style="color:red;">运行时异常</span >，不需要做任何处理

​											如果时<span style="color:red;">检查型异常</span>，必须要配合try catch或者throws使用



###### 自定义异常：

继承Throwable及其子类去编写

```java
public class AgeException extends Exception{
    public AgeException(){
        super("年龄不符合条件")
    }
    public AgeException(String message){
        super(message);
    }
}
```

