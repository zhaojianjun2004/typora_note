### day2 

一.

1.boolean类型默认值为<font color='red'>false</font>

2.字符型char，在定义变量时可以和ASCII码转换。

```
char c=97;
System.out.println(c);
//输出为a,这里把97转换成ASCII码对应字符
```

3.字符串为一种引用类型（String来声明）

   特殊转义字符：\t 制表符（跳8个字符间隔）

​							\r 回车

​							\n 换行符

4.<font color='red'>final关键字</font>修饰常量，不可以修改

​	记住在使用final关键字修饰的时候还要加入变量的数据类型

5.编码风格：

> - 类名：每一个单词首字母大写
>
> - 变量名、包名、方法名：第一个单词小写，后面单词首字母大写
> - 常量：全部大写

6.逻辑运算符：<font color='red'>针对布尔类型操作，结果只能是真或假</font>

> 逻辑与&, |, !, 逻辑异或 ^*（两边相同返回false）*,       短路或||*(如果左侧为true，则右侧不运算)*,短路与&&*(如果左侧为false，则右侧不运算，直接返回false)*

 按位运算符：<font color='red'>将数字转成二进制，按位运算，只能计算整数，不能处理浮点数</font>

>按位与&, |, ^， 按位取反~

 移位运算符：对<font color='red'>二进制数</font>位整体做移动，再补零（可以高效处理运算）

> \>>,   <<,      无符号右移>>>
>
> ```
> int a=10; //二进制表示00001010
> int b=a>>1;  //右移一位 00000101表示为5，相当于除以2
> int c=a<<2;  //左移2位，相当于乘以4，表示为40
> ```

算术运算符没有^和**表示的幂运算，使用<font color='red'>Math.pow(x,y)</font>表示x的y次方

7.三元运算符（条件运算符）：

  变量 =表达式1？表达式2：表达式3



二.

1.顺序结构

2.分支结构（选择结构）

（1）if

```
if(boolean类型表达式){
	条件成立执行的代码块
}
```

​	if  else

​	if      else if     else

​	嵌套使用

（2）switch分支

```java
switch(变量){ 不能是boolean类型
	case 常量1：操作  ；break；
	case 常量2：
	···
	default:
	//常量类型必须是声明的类型
}
```

​	简洁用法：当条件分支下执行的代码相同时，可以合并

```
case 1:
case 2:
case 12:
	System.out.println("冬天”);
	break;
```



3.循环结构

（1）while循环

```
while(boolean类型){
	当条件成立，反复执行这段代码
}
```

（2）do while循环

```
do{

}while(boolean类型值);
```

(3)for循环

```
for(赋初始值;条件判定;让循环变动){
	循环体
}
```

（小技巧：<font color='red'>fori可以快速生成for循环结构）</font>

（4)continue,break

(5)带标号的continue和break

```
out：
...
（这里有一个循环）	if(  ){
		continue out;结束本次循环，从标号的位置执行下一次循环
		//break out退出标号的循环
    }
```

