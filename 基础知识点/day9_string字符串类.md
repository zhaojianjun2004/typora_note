### day9

#### 一.String字符串类

1.字符串是一种引用类型，

​	String是final修饰的终结类，没有子类

String类对象的内容一旦初始化，不能改变（想改变，就使用StringBuffer或者StringBuilder）

使用final的byte数组来存储值

2.String是java定义好的一个类，定义在java.long包中，不需要导包

##### 3.创建：

静态创建：直接赋值`String str="abc"`在方法常量池里产生唯一一个字符串对象，如果另外一个引用指向了相同的字符串，则两个引用变量的地址相同

动态创建：`String str=new String("abc")`在堆内存会产生一个不同的对象，会产生两个对象

​				创建含有相同字符串的两个对象，会开辟不同的堆空间



##### 4.构造方法：

空参、字符串、char类型数组、byte类型数组

```
new String(char类型数组，数组下标起始位置，取出数组的长度)
```



##### 5.常用方法：

| 方法                                                  | 说明                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| equalsIgnoreCase(String)                              | <span style="color:red;">不区分大小写</span>比较字面量是否相等 |
| indexOf(String [,int])                                | 查找给定值在字符串中（给定索引位置开始）第一次出现的下标位置 |
| lastIndexOf(String [,int])                            | 查找给定值在字符串中（给定索引位置开始）最后一次出现的下标位置 |
| toUpperCase()/ toLowerCase()                          | 将字符串中的所有字符转换成大写（小写）                       |
| charAt(int)                                           | 返回下标引处的char值                                         |
| <span style="color:red;">substring(int [,int])</span> | 对字符串进行<span style="color:red;">截取</span>，从指定位置开始，（截取到结束位置（不包含）） |
| trim()                                                | 将字符串前后空格去除                                         |
| concat(String)                                        | 字符串连接。（如果是null值不能使用，并且只能传字符串作为参数） |
| getBytes()  /toCharArray( )                           | 将字符串转换为byte数组 /char数组                             |
| contains(String)                                      | 返回boolean类型，判断字符是否包含给定值                      |
| startsWith(String[,int])  /endsWith                   | 判断字符（从索引开始）是否以给定值作为开始（结束）           |
| replace(CharSequence,CharSequence)                    | 将字符序列或字符替换                                         |
| split(String)                                         | 按给定的正则表达式分割符，将字符串分隔成字符串数组           |
| <span style="color:red;">matches(String)</span>       | 判断字符是否可以和匹配给定的正则表达式                       |
| ContentEquals()                                       | 字符串与StringBuffer或者字符序列比较内容                     |

------



#### 二.正则表达式

- 正则表达式又称规则表达式，是一种文本模式，包括<span style="color:red;">普通字符和特殊字符</span>（元字符）。

- 通常用来检索、替换某个模式（规则）的文本

##### 1.目的：

- *给定一个正则表达式，判断给定的字符串是否符合正则表达式的过滤逻辑*
- *通过正则表达式，从字符串中获取我们想要的特定部分（提取）*

| 实例              | 描述                                                    |
| ----------------- | ------------------------------------------------------- |
| rub[ye]           | 匹配"ruby"或"rube"                                      |
| [abcdef]          | 匹配括号中的任意一个字母                                |
| [0-9]或\d         | 匹配任何数字                                            |
| [a-zA-Z0-9]或者\w | 匹配任何字母和数字（匹配包括下划线的任何字符单词）      |
| [^au]             | 匹配除了au字母以外的所有字符                            |
| [^0-9]或\D        | 匹配除了数字以外的字符                                  |
| .                 | 匹配除\n之外的任何单个字符                              |
| ?                 | 匹配一个字符零次或一次，另一个作用是非贪婪模式          |
| +和*              | 匹配1次或多次（匹配0次或多次）                          |
| \b                | 匹配一个长度为`0`的子串                                 |
| \s和\S            | 匹配任何空白字符，包括空格、制表符、换页符等/（非空白） |



------

#### 三.StringBuffer

内容可变的字符串类，对字符串的内容进行动态操作，不会产生额外的对象

初始时，默认有16个字符来做缓冲区

方法有synchronized修饰，线程安全

##### 1.构造方法：

参数可以无参、String、int、CharSequence（接口）

##### 2.常用方法：

| 方法                                       | 描述                                             |
| ------------------------------------------ | ------------------------------------------------ |
| append()                                   | 在当前StringBuffer对象上，追加其他内容           |
| capacity()                                 | 返回当前容量                                     |
| length()                                   | 返回长度                                         |
| setCharAt(int,int)   /deleteCharAt(int)    | 指定位置的字符设置为给定值/（删除指定位置字符）  |
| reverse()                                  | 将StringBuffer内容反转                           |
| delete(int,int)                            | 删除从指定索引（包含）到结束位置（不包含）       |
| <span style="color:red;">toString()</span> | 将对象转成字符串                                 |
| insert(int,Object)                         | 在指定位置插入给定值                             |
| replace(int.int,String)                    | 将起始索引（包含）到结束索引（不包含）的内容替换 |



#### 四.StringBuilder

提供了和StringBuffer相同的API

方法没有synchronized修饰，非线程安全，如果是单线程操作字符串相关处理，StringBuilder效率更高

- String和StringBuffer区别：一个是常量，一个是变量。经常堆字符串进行修改、删除、插入操作，使用StringBuffer效率更高，String使用final的byte数组来存储值，一旦创建不能改变
- StringBuffer和StringBuilder：前者有线程安全，后者非线程安全