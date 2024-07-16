## day30 注解

### 一.注解

#### 1.概念：

Annotation（注解）:主要用于修饰类、方法或变量

注解的定义：

```java
public @interface TestAnnotation{
} //注解通过@interface关键字进行定义
```

注解的使用：

```java
@TestAnnotation
public class Test{
} //将TestAnnotation这个注解应用到Test类上面
```



#### 2.应用：

##### 2.1 生成文档

##### 2.2 跟踪代码依赖性

实现替代配置文件功能，使用注解的作用是减少配置，在反射的Class,Method,Field这些方法中，也有很多Annotation的处理



#### 3.注解分类：

##### 3.1  内置注解

##### 3.2  元注解

元注解理解为对其他注解进行标签化的注解

**五种类型**：

##### @Retention ：解释了注解的存活时间

取值如下：

> - RetentionPolicy.SOURCE 只保留在源码阶段
> - RetentionPolicy.CLASS   只被保留到编译阶段，不会进入JVM
> - RetentionPolicy.RUNTIME 保留到程序运行的时候，会进入JVM
>
> 语法：@Retention(RetentionPolicy.RUNTIME)

##### @Documented   ：将注解的元素包含到 javadoc中去

> javadoc：文档注释通过Javadoc生成相应的API帮助文档，主要用来说明类、成员变量和方法的功能
>
> 可以从程序源代码中抽取类、方法、成员等注释，然后形成一个和源代码配套的 API 帮助文档

##### @Target   ：指定了注解运用的地方

取值：

> - ElementType.ANNOTATION_TYPE 可以对一个注解进行注解
> - ElementType.CONSTRUCTOR 给构造方法注解
> - ElementType.FIELD 给属性注解
> - ElementType.LOCAL_VARIABLE 可以给局部变量进行注解
>
> 其余的METHOD方法，PACKAGE包 ，PARAMETER方法内的参数 ，TYPE给一个类型进行注解（类，接口，枚举）

##### @Inherited  ：继承

> 不是注解可以继承，而是当一个注解被@Inherited进行注解，然后一个超类被这个注解进行注解，如果这个超类的子类没有被任何注解应用的话，那么这个子类就继承了这个超类的注解
>
> ```java
> @Inherited
> @Retention(RetentionPolicy.RUNTIME)
> @interface Test{}
> @Test
> public class A{ }
> public class B extend A { }
> ```

##### @Repeatable  ：可重复

注解的值可以同时取多个的情况，那么这个注解就可以多次应用



##### 3.3  自定义注解

定义格式和使用格式

> public @interface 注解名{}

> @注解名

###### 3.3.1.注解的属性：

```java
//简单理解，注解只有属性没有方法
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface TestAnnotation{
    int id();
    String msg();
}
//没有初始值的时候就需要赋值
@TestAnnotation(id=3,msg="hello annotation")
public class Test{
}
```

初始值不想在需要的时候进行赋值，那么就需要默认初值，使用default关键字指定

```java
@Target(ElementType.TYPE)
@Retention(Retention.RUNTIME)
public @interface TestAnnotation{
    public int id() default -1;
    public String msg() default "hi";
} //调用的时候就不需要使用再使用括号赋值了
@TestAnnotation()
public class Test{}
```

其次如果没有属性，那么连括号都不需要

```java
public @interface Perform{}
@perform
public void TestMethod(){}
```





### 二.基于JDK动态代理

#### 1.简介：

动态代理就是在不修改原有代码的情况下，为程序添加新的功能，实现程序功能的增加

分类：

- JDK动态代理
- CGLIB代理

#### 2.JDK动态代理API

- InvocationHandler接口
- Method类
- Proxy类

> jdk的动态代理目标类必须要有接口

#### 3.实现步骤

1.创建接口

2.创建目标类实现接口

3.创建`InvocationHandler`接口的实现类，在`invoke`方法中完成代理功能