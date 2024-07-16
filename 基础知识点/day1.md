### day1

1.cmd终端：执行javac  文件名.java

​	                   执行java  文件名

​	*如果出现乱码，转成<font color='red'>ANSI格式编码</font>（这是对ASCII码的拓展编码）*

2.java程序执行：javac命令是将源代码编译成class字节码文件，java来运行class字节码文件

> JVM虚拟机执行class字节码文件（只执行<font color='red'>含有main方法</font>的class文件）（main方法是java程序的入口）

3.文档注释：/**            javadoc生成说明文档 html

​							*

​						*/

4.变量类型：8种基本数据类型（*byte, boolean, short, char int, float, double*），引用类型

> - JDK10之后的一种变量声明方式：<font color='red'>var 变量名=值</font>（这里必须赋初始值）
>
> - 这种声明方式自动推断数据类型
>
> - 一般情况为了阅读不使用

​	数据类型转换：小转大自动转换，大转小有精度误差

<font color='red'>注意：</font>不要比较float和double类型，有精度差异

- 数据类型默认为int类型，有时需要强制转换类型

5.标识符：标识符不能以数字开头

6.使用工具类：

- ​	import导入

  Scanner类：import   java.util.Scanner;

  ​					···

  ​					Scanner scanner=new Scanner(System.in);

  ​					System.out.println("请录入数字：")；

  ​					int x=Scanner.nextInt();

  ​					···

