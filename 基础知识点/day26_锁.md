## day26

### 一.数据共享的问题

#### 1.问题分析：

临界区：一段代码之间，如果存在对共享资源的多线程读写操作，这段代码称为临界区

> 注意：当一个对象或者一个不同步的共享状态，被两个或两个以上线程同时修改时，对访问顺序必须严格执行，否则会产生<span style="color:red;">竞态条件</span>



#### 2.问题解决

<span style="color:red;">同步代码块</span>：将操作共享数据的代码锁起来

> 特点：
>
> - 锁默认打开，有一个线程进去了，锁就自动关闭
> - 里面的代码全部执行完成，线程出来，锁自动打开

`synchronized`锁

对象锁的概念，简单来说就是让同一时间点只能由一个线程执行，保护当前拥有锁的线程安全执行临界区中的代码

```java
//锁对象：注意一定要是唯一的
synchronized(对象){
    //临界区代码
}
```

> 共享数据：`static`关键字修饰成静态变量，表示为这个类所有的对象都共享这个数据
>
> <span style="color:red;">线程创建时，可以使用lambda表达式来线程执行的任务</span>
>
> ```java
> Thread t1=new Thread(()->{
>     synchronized(obj1){//obj1是要锁的对象
>         for(int i=0;i<1000;i++){
>             x++;//四行字节码
>         }
>     }
> })
> ```

```java
//锁实例方法
public synchronized void decrement(){
    x--;
}
//相当于
public void increment(){
    synchronized(this){
        //执行代码；
    }
}

//锁类方法
//注意，在static方法里面不能使用this
public synchronized static void test(){}
//相当于
public static void test1(){
    synchronized(Numberobj.class){
        
    }//使用.class当前类的字节码文件对象
}
```



#### 3.Monitor监视器

`Monitor`理解为监视器或者管程

有`WaitSet``EntryList``Owner``MarkWord`

#### 4.线程通信wait/notify

方法：

- wait()方法，让加入obj监视器的线程到waitset中等待，直到另一个线程调用此对象的notify()或者是notifyAll()唤醒，或者到了指定时间

  > wait是Object类的方法

- notify()方法，在obj监视器上正在waitset等待的线程中选择一个激活

- notifyAll()方法，所有的waitset等待的线程全部激活

- 都属于Object类的方法，必须获得对象的锁才能使用

