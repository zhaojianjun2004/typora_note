day27

### 一.ReentrantLock

1.可重入的互斥锁，比`synchronized`更加灵活，具有更多的方法

```java
reentrantlock.lock();//加锁
try{
    //代码
}finally{
    reentrantlock.unlock();//解锁
}
```

2.特点：

- ##### 支持可重入

加了几次锁就要释放几次，`reentrantlock.lock()`和`reetrantlock.unlock()`

- 可中断

`lock.lockInterruptibly()`可被中断

`thread.interrupt()`线程中断操作

```java
//执行操作
Thread thread=new Thread(()->{
    try{
        System.out.println("线程尝试获取到锁");
        //lock.lock();
        lock.lockInterruptibly();//可被打断
    }catch(InterruptedException e){
        System.out.println("线程被中断");
        return;
    }//try...catch接线程获取到锁和释放锁
});
thread.start();
if(thread.isAlive()){
    System.out.println("执行线程中断操作");
    thread.interrupt();
}else{
    System.out.println("线程执行完成");
}
System.out.println(lock.isLocked);
```



- 可以设置超时时间

`lock.tryLock(3,TimeUnit.SECONDS)`，

> 尝试拿到锁，在一个时间范围内，如果超过时间还没有获得锁就认为获取锁失败

- 可以设置公平锁和非公平锁

> 公平锁可以让所有线程都得到资源，避免出现线程饥饿问题，但是队列里除了第一个线程，其他线程都会阻塞，那么cpu唤醒阻塞线程的开锁很大，吞吐量会下降很多

> 非公平锁的优劣点和前面相反

```java
//步骤是创建一个Fair线程，在线程里面
```



- 支持多个条件变量，相当于多个waitset

> `waitset`是一个对象的属性，用来存放调用了该对象的wait()方法之后进入了block状态的线程



#### Condition

和`ReetrantLock()`一起使用的，和`wait/notify`相同的作用

主要调用的方法：

- await：使线程进入等待，同时释放锁，当其他线程使用到singal方法的时候，线程会出现获得锁并继续执行
- singal：唤醒一个正在等待的线程
- singalAll：会唤醒所有的线程



### 二.线程池

#### 1.说明：

线程池里存放了很多可以复用的线程，可以用线程池来维护多个线程，进行统一管理

创建一定数量的线程放在线程池里面备用，比需要时创建开销小，更块（节省了创建线程和销毁线程的时间）

#### 2.状态：

5种状态：`RUNNING`  （线程池初始状态）,

  `SHUTDOWN`, （调用了线程池`shutdown`方法）

  `STOP`  ,（调用了线程池`shutdownNow`方法，中断正在执行的任务）

> RUNNING可以‘接受新任务''和''处理阻塞队列''，
>
> SHUTDOWN不能接收新任务，但能处理阻塞队列
>
> STOP都不能

`TIDYING`. 活动线程数为0，即将终结

`TERMINATED`终结状态



#### 3.基本架构：

##### 	3.1 ThreadPoolExecutor

##### 



#### 4.通过工厂方式创建线程池：

`Executors`静态工厂类，返回`ExecutorService`、`ScheduledExecutorService`等线程池对象

`Executor`没提过execute（）方法来执行已提交的Runnable目标实例

##### 	4.1 固定线程池`newFixedThreadPool`



##### 	4.2 单线程化线程池`newSingleThreadExecutor`



##### 	4.3 可缓存线程池`newCachedThreadPool`



##### 	4.4 任务调度线程池`newScheduledThreadPool`



