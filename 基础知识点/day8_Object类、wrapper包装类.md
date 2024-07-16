### day8（api和包装类）

#### 一.API(应用编程接口)

#### 二.Object

1.java中所有类的父类，object没有父类

​	object类中的所有方法都可以被子类继承

2.object<span style="color:red;">只有空参构造方法</span>`public Object()`

3.常用方法：

- `public String toString()`    返回对象的字符串形式
- `public boolean equals(Object obj)`    比较两个对象是否相等
- `protected Object clone(int a)`    对象克隆
- 





#### 三.Wrapper类（包装类）

1.提供包装将（基本数据类型）封装成（对象）来操作

2.基本数据类型可以通过包装类和String类做转换

3.基本数据类型和包装类：

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| int          | Integer   |
| short        | Short     |
| char         | Character |

其他的均将首字母大写即可

##### 4.常用方法：

获取最大值MAX_VALUE、最小值MIN_VALUE



