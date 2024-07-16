# day29 反射

### 一.反射机制

#### 1.简介：

1.1 反射机制的核心是在程序运行时动态加载并获取类的详细信息，从而操作类或对象的属性和方法。

本质是JVM得到class对象之后，再通过class对象进行反编译，从而获得对象的各种信息。

1.2 通过反射，可以动态地创建对象并调用其属性，不需要提前在编译期知道运行的对象是谁

> 如果知道类或对象的具体信息，那么就直接操作，如果不知道，就需要使用java反射机制动态获取类的信息。

### 2.class类

.class字节码文件，在载入时会产生一个java.lang.Class对象代替.class文件

Class类是反射机制的基础



### 3.获得Class对象

#### 3.1 方法一：

使用Class类的静态方法forName(String className)，参数className表示所需类的全路径

```java
Class<?> clazz=Class.forName("com.coder.Student");
```

#### 3.2 方法二：

使用类名来调用class属性，获取该类的Class对象，	`类名.class`

```java
Class<?> clazz=Student.class;
```

#### 3.3 方式三：

使用该类的对象调用getClass()方法，来获取该类对应的Class对象

```java
Student student=new Student();
Class<?> clazz3=student.getClass();
```

#### 3.4 方式四：

使用类的装载器

```java
ClassLoader loader=Student.class.getClassLoader();
Class<?> clazz4= loader.loadClass("com.coder.Student");
```



<!--注释-->

一般情况使用反射获取一个对象的步骤：

- 获取类的Class对象

```java
Class clz=Class.forName("com.zhenai.api.Apple");
```

- 根据Class对象实例获取Constructor对象

```java
Constructor appleConstructor= clz.getConstructor();
```

- 使用Constructor对象的newInstance方法获取反射类对象

```java
Object appleObj= appleConstructor.newInstance();
```

如果要调用某个方法，则需要经过下面的步骤：

- 获取方法的Method对象：
- 利用invoke方法调用方法：



<!--newInstance方法-->

> 为什么使用newInstance方法来创建对象？

假设定义一个接口Car，汽油车为OilCar（类）

后来生产了电车EnergyCar（类），为了能方便转换，那么就出现了工厂设计模式

后续为了再方便工厂切换车辆生产类型，就出现了newInstance方法，通过修改配置文件（properties）来变换





### 4.反射获取泛型和接口、超类

#### 4.1 反射获得泛型：

<span style="color:red;">不可以通过反射获得局部变量的泛型</span>

#### 4.2 获取接口和超类：





### 5.Constructor类：

获取无参构造方法：`aClass.getConstructor()`

调用带参数的构造方法：`aClass.getConstructor(String.class,int.class)`

>```java
>Constructor<?>constructor=aClass.getConstructor(String.class,int.class);
>Object o=constructor.newInstance("李白",20);
>Student student=(Student) o;
>System.out.println(student);
>```

访问私有构造方法：`Constructor<?> constructor= aClass.getDeclaredConstructor()`

> `setAccessible(true)`取消java语言对访问的检查
>
> field类实例也可以使用这个`field.setAccessible(true)`

访问构造方法数组：`Constructor<?>[] declaredConstructors=aClass.getDeclaredConstructors()`





### 6.Field类：

field类描述的是类的<span style="color:red;">属性信息</span>

#### 6.1 如何获取Field类对象

- `getField(String name)`  name参数指明属性名称（获取单一属性）
- `Class.getFields() `    获取类中public类型的属性，返回一个包括某些Field对象的<span style="color:red;">数组</span>，该数组包括含此Class对象所表示的类或接口的所有可访问字符
- `getDeclaredField(String name)`    获取类特定的方法，name参数指定了属性的名称
- `getDeclaredFields() ` 获取类中的所有属性（不能获取父类的属性）

fields[ ]数组遍历获取所有的属性

#### 6.2   field类方法

- 返回field类的一个实例，描述class类的实例的一个属性

  `Field f1=cls.getDeclaredField("gender")`;//gender属性

- 获取属性名称`f1.getName()`

- 获取属性类型`f1.getType()`

- 获取访问修饰符`field.getMOdifiers()`





### 7.Method类：

获取所有本类和父类的公共方法：`Method[] methods= aClass.getMethods()`

获取本类的所有方法:`aClass.getDeclaredMethods()`

获取方法的返回值类型：`method.getReturnType()`

方法的参数：`Class<?> parameterTypes=method.getParameterTypes()`

> 这里有一个方法：`getSimpleName()`，获取简单名称，然后可以将其打印到控制台
>
> 和`getName()`的区别：getName()获取的是实体名称，例如com.coder.Student，而简单名称/（底层类名称）就表示为Student

获取方法异常列表：`Class<?> []exceptionTypes=method.getExceptionTypes()`

获取注解：`Annotation[] annotations=method.getAnnotations()`



获取一个方法并调用：

```java
Class<?> aClass=Class.forName("com.coder.Student");
Method method=aClass.getDeclaredMethod("add",int.class,int.class); //获取方法
Object obj=aClass.getConstructor().newInstance();
Object result=addMethod.invoke(obj,10,20);
System.out.println(result);
```

