## day24

### 一.文件字节流

InputStream,OutputStream

FileInputStream、FileOutputStream、BufferedInputStream、BUfferedOutputStream

> 补充：bis.read(bytes)方法尝试从输入源读取字节并将其储存在字节数组'bytes'中，它返回读取的字节数，如果到达文件末尾，输出返回-1（bis是BufferedInputStream的实例）



<!--文件复制-->

文件复制方式：字符流复制、字节流复制

> 1、使用字符流复制：使用字符流`FileReader`和`FileWriter`来复制文件

```java
//首先将reader和writer实例化
char[] chars=new char[1024];

```

> 2、使用字节流复制：使用字节流`FileInputStream`和`FileOutputStream`



### 二.对象的序列化和反序列化

#### 1.对象的序列化：

`ObjectOutputStream`完成对象序列化操作





#### 2.对象反序列化：

将字节序列重新恢复成java对象

`ObjectInputStream`完成对象反序列化操作





### 三.标准输入输出

System.in:标准输入，默认对应键盘

System.out:标准输出，默认对应显示器

System.err:标准错误输出，对应显示器



格式化输出





### 四.`ByteArrayInputStream`和`ByteArrayOutputStream`

> `ByteArrrayOutputStream`类是在创建它的实例时，程序内部创建一个byte型别数组的缓冲区，然后利用`ByteArrayOutputStream`和`ByteArrayInputStream`的<span style="color:red;">实例</span>向数组中写入或读出byte型数据。在网络传输中我们往往要传输很多变量，我们可以利用`ByteArrayOutputStream`把<span style="color:red;">所有的变量收集到一起</span>，然后一次性把数据发送出去。

ByteArrayOutputStream：可以捕获内存缓冲区的数据，转换成字节数组

ByteArrayInputStream：可以将字节数组转换成输入流

```java
Public static void main(String[] args){
    int a=0;
    int b=1;
    ByteArrayOutputStream bout=new ByteArrayOutputStream();
    bout.write(a);
    bout.write(b);
    byte[] buff=bout.toByteArray();
    for(int i=0;i<buff.length;i++)
        System.out.println(buff[i]);
    ByteArrayInputStream bin=new ByteArrayInputStream(buff);
    while((b=bin.read())!=-1){
        System.out.println(b);
    }
}
//使用toByteArray()和toString()获取数据
```





### 五.`DataInputStream`和`DataOutputStream`

不需要使用对象序列化技术时就可以使用DataInputStream和DataOutputStream来写入和读取数据操作

