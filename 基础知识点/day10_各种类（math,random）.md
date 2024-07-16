### day10

#### 一.Math类

##### 1.简介：

- Math类是使用final修饰的终结类，不能产生子类（和String类一样）
- Math类中的方法都是static修饰的静态方法，可以直接调用（`类名.方法名`）

##### 2.常用方法：

| 方法                    | 说明                                  |
| ----------------------- | ------------------------------------- |
| abs()                   | 求绝对值                              |
| ceil()  /floor()        | 求大于等于给定值的最小数/小于的最大数 |
| pow(oduble x, double y) | x的y次方                              |
| sin() /cos() /tan()     | 三角函数值                            |
| sqrt()                  | 求平方根                              |
| random()                | 获取0-1的随机小数                     |
| round()                 | 四舍五入                              |



#### 二.Random类

1.构造方法：

`Random random=new Random([long])`，创建对象时可使用种子数（long）,也可以不使用

2.Random类产生的数字是<span style="color:red;">伪随机数</span>，在相同种子数的相同次数产生的随机数是想同的

###### 3.方法：

| 方法           | 说明                                        |
| -------------- | ------------------------------------------- |
| nextInt([int]) | 获取0（包含）到给定值（不包含）之间的随机数 |
| nextfloat()    | 单精度浮点数0到1之间                        |
| nextDouble()   | 双精度                                      |
| nextBoolean()  | 随机boolean类型,true或false，概率相同       |
| nextlong()     |                                             |



#### 三.BigInteger和BigDecimal

##### 1.简介：

- BigInteger可以支持任意长度的整数；(比long的取值范围更大)
- BigDecimal可以支持任意精度的浮点数
- 用来做<span style="color:red;">精确计算</span>

##### 2.创建方式：

`new Integer`([参数1，进制]);（将不同进制转成10进制）

`BigInteger.valueOf(int val)`;//BigInteger类的一个静态方法，用于创建一个'BigInteger'对象

Scanner对象的`nextBigInteger()`   ` nextBigDecimal()`;

```java
BigInteger bigInteger=BigInteger.valueOf(233432);
```

##### 3.方法：

大多数方法的参数必须是对应BigInteger类型或BigDecimal类型。不能是其他类类型或基本数据类型

如果遇到报错的情况，参数定义改为`new BigInteger(数据)`

| 方法                        | 说明                                                |
| --------------------------- | --------------------------------------------------- |
| add()  /substract()         | 加法/ 减法                                          |
| intValue()   /doubleValue() | 将BigInteger转成int类型（BigDecimal转成double类型） |
| multiply()  /divide()       | 乘法  /除法                                         |
| remainder()                 | 求余数                                              |
| divideAndRemainder()        | 求除法商和余数，返回的是BigInteger数组              |
| max () /min()               | 最大值/最小值                                       |

##### 4.RoundingMode处理方式:

- `UP和DOWN`：

​	Rounding.UP:向远离零点方向舍入 （1.4舍入到2(假如保留到整数)）

​	Rounding.Down:向零点方向舍入（截断数字）

- `CEILING和FLOOR`：

​	CEILING：向正无穷方向舍入

​	FLOOR：向负无穷方向舍入

- `HALF_UP和HALF_DOWN和HALF_EVEN`：

  这个就要判断舍入那一位数字和5之间的大小关系；

  HALF_UP:向远离零点方向舍入（通常意义上的四舍五入）

  HALF_DOWN:向零点方向舍入（如果到两个相邻的数字距离相等，那么向零点方向舍入。其他时候四舍五入）（例如1.5->1）

  HALF_EVEN:取最近两个数中的偶数

##### UNNECESSARY：

​	当要处理的那一位数字为0的时候不抛出异常，并进行处理

​	(例如：1.2 throw ArithmeticException，

​				1.0不抛出异常)

------



#### 四.Enum枚举

1.从给定值中列举，通常是有固定值，来做选择

`[修饰符] enum 枚举名{}`

2.所有的枚举类型，都是继承了java.lang.Enum类

3.常用方法：

| 方法        | 说明                             |
| ----------- | -------------------------------- |
| values()    | 以数组形式返回枚举类型的所有成员 |
| valueOf()   | 将字符串转换为枚举类型           |
| ordinal()   | 获取枚举成员的索引               |
| compareTo() | 比较两个枚举成员在定义时的顺序   |

4.枚举常量通常使用<span style="color:red;">大写和下划线</span>

------



#### 五.Timer

`timer.schedule(new TimerTask()`{}方法执行时间运行任务

```java
Timer timer=new Timer();
timer.schedual(new TimerTask(){
    @Override
    public void run(){
        System.out.println("输出内容")
    }
}0,1000)//0到1000毫秒（1秒）
```



------



#### 六.System

java.lang.System系统

###### 1.方法：

| 方法                                  | 说明                          |
| ------------------------------------- | ----------------------------- |
| getProperty(String)  /getProperties() | 获取系统属性/（所有系统属性） |
| getenv(String)                        | 获取指定环境变量              |
| exit(0)                               | 0为正常退出java虚拟机         |

###### 2.`system.getProperty(propertyName)`

​	如果要获取操作系统的名称，可以使用以下代码：

```java
String osName=System.getProperty("os.name");
```

