### day11

#### 一.Data类：

`java.util.Data`表示指定的时间信息，不支持国际化

和System类有差异：`java.lang.System`

##### 1.构造方法：

new Data([long])：给定日期和时间；

##### 2.主要方法：

| 方法                        | 说明             |
| --------------------------- | ---------------- |
| after(Data)   /before(Data) | 判断当前日期对象 |
| equals(Object)              |                  |
| compareTo(Data)             |                  |



------

#### 二.DataFormat:（日期格式化类）

对日期类进行<span style="color:red;">格式化和解析</span>

本质上是一个抽象类



<!--抽象类型知识回顾-->

> 抽象类型主要表现为`接口`和`抽象类`
>
> - 接口（Interface），是抽象方法的集合（对事物的局部行为进行抽象）
> - 抽象类：一个类中没有足够的信息来描述一个具体的对象，这样的类就是抽象类（是对事物的整体进行抽象）
>
> 接口是like a或者has a的关系； 抽象类是is a的关系
>
> > 例如飞行可以作为一个接口，飞机和鸟都可以作为一个抽象类，然后战斗机和直升机可以作为飞机抽象类的子类



##### 实例化的方式：

- 静态方法的调用：处理长日期和长时间类型

  getDataInstance():

  getTimeInstance():

  getDataTimerInstance():

- 创建子类对象：处理短日期和短时建类型

  



------

#### 三.Calendar

抽象类



------

#### 四.GregorianCalendar

格里高利历：公历

判断闰年的方法：isLeapYear(int),返回一个boolean类型的值

------

#### 五.JDK8新增日期工作类

LocalData:获取本地日期

LocalTime:获取本地时间

LocalDataTime:获取本地日期和时间

```java
LocalData data=LocalData.now();//获取当前系统时间

LocalData data1=LocalData.of(2024,4,9); //自定义设置系统日期和时间
```

##### 单独获取日期时间类的每个值：.getXXX

```java
LocalDataTime datatime=LocalDataTime.now();

int year=dataTime.getYear();//获取年份
int dayOfMonth=dataTime.getDayOfMonth();//获取第几天

DayOfWeek dayOfWeek=dataTime.getDayOfWeek();//这是另一种形式，使用抽象类类型定义的变量，最后要使用.getValue()来获取值
System.out.println(dayOfWeek.getValue());//获取星期几

//获取小时，分钟，秒钟，就使用对应的getHour(),getMinute(),getSecond()
```

##### 给定值修改日期：withXXX

具体实现：

`withYear() ` 修改年

 `withDayOfMonth()`修改日期为一个月的第几号

`withDayOfYear()`修改日期我i

```

```

##### 设置日期和时间的偏移量：

`plusDays()`,`plusYears()`...

可以作为时间的一个截止日期或分割线

```

```

##### Instant类：

代表时间点，获取日期变更子午线时间

涉及到`时间戳`的获取



##### DataTimerFormatter格式化和解析

*一般时间的格式化和解析单独放一个类来实现*



##### Period计算两个“日期”之间的间隔，得到的是年月日

实现方式为`Period.between(day1,day2)`

具体多少天需要使用`ChronoUnit.DAYS.between(day1,day2)`:直接将结果赋值给变量，变量类型一般为long

具体·多少年月把`DAYS`改了即可

如果想获取具体的年月日使用相应的 `getYears()`...即可（复数加一个s即可）

​							或者`toEpochDay()`

```java
//toEpochDay()的计算代码示例：
LocalData data1=LocalData.of(2021,1,1);
LocalData data2=LocalData.of(2023,1,1);

long daysBetween=data2.toEpochDay()-data1.toEpochDay();
```



##### Duration计算两个“日期时间”的间隔：



##### 时间调节器：

###### `TemporalAdjusters`（注意是复数）





##### `Data`类和`LocalData`(` LocalTime`\``LocalDataTime` )转换

