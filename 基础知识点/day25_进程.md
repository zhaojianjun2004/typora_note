## day25

### 一.进程和线程

#### 1.进程

简单理解，可以看作程序的一个实例，一些程序可以同时运行多个实例进程，有些只能启动一个

#### 2.线程

一个进程之内可以分一到多个线程

<!--补充-->

线程是最小调度单位，进程是资源分配的最小单位

进程不活动，作为线程的容器

>多线程：同时做多个事情，提高效率，
>
>​				软件中的耗时操作，所有的聊天软件，所有的服务器

```java
Thread t2=new Thread(()-> {
    FileUtil.readFile();
    FileUtil.readFile();
},"t2");//这个代码的()->{}是lambda表达式的简洁版，用于定义线程执行的任务，后面t2表示线程的名称
```



#### 3.并行与并发

并发：同一时刻，多个指令在单个cpu上交替执行

并行：同一时刻，多个指令在<span style="color:red;">多个</span>cpu上同时执行



#### 4.多线程的实现方式：

- ##### 继承Thread类（线程）

要实现线程，就实例化Thread类

```java
//自己写一个类继承Thread类
//重写run方法
//创建子类的对象
public class MyThread extends Thread{
    @Override
    public void run(){
        //书写要执行的代码
        for(int i=0;i<100;i++){
            System.out.println("Hello")
        }
    }
}
```

`start()`打开线程

可以使用MyThread类实例来调用setName()方法来起名

- ##### 实现Runnable接口,重写run方法

```java
class MyThread implements Runnable{
    @Override
    public void run(){
        //需要执行的代码
    }
}
```

<!--解释-->

`Runnable`是一个接口，只声明了一个run()方法

```java
public interface Runnable{
    public abstract void run();
}
```

`Callable`是一个泛型接口，`call()`函数返回的类型就是传递进来泛型

`Future`就是对具体的Runnable或者Callable任务的执行结果进行取消、查询是否完成、获取结果，必要时可以通过get()方法获取执行结果，该方法会阻塞直到任务返回结果

`FutureTask`是`Future`的具体实现类，`Future`只是一个接口，无法实例对象，`FutureTask`是`Future`接口的唯一实现类



- ##### FutureTask配合Callable

Future是jdk1.5引入的一个interface，用于异步获取结果，表示一个可能还没有完成的异步任务的结果，针对这给结果，可以添加回调处理，以在任务执行成功或失败后做出相应的操作

`Future`接口声明了几个方法：

| 方法                              | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| boolean cancel(boolean)           | 取消任务，如果取消成功就返回true,否则返回false               |
| boolean isCancelled()             | 判断任务是否在执行前被取消成功（返回true的原因，可能是在任务执行之前被调用了cancel()方法进行取消） |
| isDone()                          | 任务是否完成，正常终止、异常、取消，都认为是任务完成         |
| V get()                           | 获取计算结果                                                 |
| V get(long timeout,Timeunit unit) | 获取计算结果，超时时间                                       |



#### 5.查看进程：

windows系统：

- tasklist 查看进程
- taskkill 杀死进程

jps查看所有java进程

jstack：生成jvm当前时刻所有线程快照



#### 6.线程的状态

##### 6.1 操作系统层面划分

五种状态

##### 6.2 编程语言层面划分

六种状态

- `NEW`  线程刚常见对象，还没有调用start()方法
- `RUNNABLE`   调用了start()方法

可细分为三种状态：`BLOCKED`     ` WAITING  `    `TIMED_WAITING`都是在java层面对阻塞状态的细分情况

- `TERMINATED` 当前线程执行结束

