## day23

### 文件管理

#### 1.File类

java中对文件和目录使用`java.io.File`来管理

主要是针对文件和目录进行管理，信息查看、文件和目录的删除、创建等

##### 三种构造方法：

文件创建时，不给出根目录相对路径就默认从当前工作目录开始解析

./的形式

相对路径和绝对路径根据需要来选择

```java
//创建目录和文件
//第一种
File file=new File("d:/aa");
File file=new File("d:/aa/hello.txt");//直接在目录后面添加路径创建文件

//第二种
File file=new File("d:/aa","bb");//多加一个参数作为文件
File file=new File("d:/aa","hello.txt");

//第三种
File dir=new File("d:/aa");//明确创建一个目录
File file=new File(dir,"hello.txt");
```

> 创建文件

`createNewFile()方法`

创建临时文件`createTempFile()`



> 创建目录

`mkdir()`方法

`mkdirs()`方法



> 文件删除

`deleteOnExit()`

```java
//创建一个临时文件
File tempFile=File.createTempFile("Order_",".txt");
//当虚拟机退出时，删除文件
tempFile.deleteOnExit();
System.out.println(tempFile.getAbsolutePath());//获取文件完整路径的方法
```



> 删除目录



###### 其他方法

`getName()`获取文件名

`getParent()`获取目录名

`length()`获取文件大小		

`file.setWritable(false)`设置文件只读

`file.canExecute()`测试文件是否可执行     `file.canRead()`是否可读       `file.canWrite()`是否可写

`file.getPath()`  获取在File类构造方法给的路径      `file.getAbsolutePath()` 获取绝对路径    

`file.getCanonicalPath()`精准获取绝对路径方式，可去除在构造是给的相对路径

`file.isHidden()`判断文件是否隐藏文件

`oldname.renameTo(new File("路径"))`对文件重命名，可以将文件命名到其他目录或者盘符下，可以实现文件剪切工作（返回boolean类型）

`File.listRoots()`获取所有磁盘分区

```java
File[] disks=File.listRoots();
for (File disk:disks){
    System.out.println(disk);
}
```

获取磁盘空间操作：

`file.getTotalSpace()`获取磁盘分区总容量

`file.getFreeSpace()`获取分区自由空间的大小（剩余空间）

`file.getUsableSpace()`获取jvm可用空间大小

`file.lastModified()`获取文件最后修改时间戳

​			这个一般如果要获取时间的话，还得转换格式LocalData类转换成Data类



### IO流

#### 1.分类

- 按流的方向划分：输入流、输出流
- 按处理数据单位划分：字符流、字节流
- 按功能不同：节点流、处理流

#### 2.主要流的API：

字节流：InputStream:输入流

​				OutputStream:输出流

字符流：Reader:输入

`Reader.readLine()`

​				Writer:输出

#### 3.文件操作流：

`FileReader`:读取

`FileWriter`：字节流+编码表

> 一般在实例化FileReader或者FileWriter之后使用BufferedReader和BufferedWriter来包装对象，可以实现缓冲读取，提高效率
>
> BufferedReader会在内部维护一个缓冲区，每次读取时先将数据读入缓冲区，从缓冲区中读取数据，减少对磁盘的访问次数，提高效率

<!--文件写入-->

两种方式，一种直接写入，一种使用try-with-resourse

> 直接写入：
>
> ```java
> FileWriter writer=new FileWriter("d:/aa/hello.txt");
> writer.write("欢迎");
> //writer.flush是强制写入，行数就使用file.newLine()方法换行
> //使用BufferedWriter或者其他缓冲Writer写入数据的时候，数据可能不会立即写入目标文件，相反，数据可能会缓冲在内存中，提高性能并减少写入操作的数量，使用flush强制将缓冲区中的所有数据（在这之前的）写入文件，而不是等缓冲区自动刷新
> ```
>
> 使用try-with-resource方法
>
> ```java
> try (FileWriter writer = new FileWriter("d:/aa/hello.txt")) {
>     for (int i = 0; i < 10000; i++) {
>         writer.write(i + "\t");
>     }
>  } catch (IOException e) {
>     e.printStackTrace();
> ```



`FileInputStream`:

`FileOutputStream`



##### 4.文本文件复制：

`copy(a,b)`将a文件复制到b文件,使用File类创建

`copyBuffer(a,b)方法`使用String类型创建(本质是一个读，一个写)

```java
//copyBuffer方法实现
FileReader reader=new FileReader(srcFile);//src是String类型的形参
FileWriter writer=new FileWriter(desFile);//也是String类的形参
BufferedReader bufferedReader=new BufferedReader(reader);
...;
String str;
While((str=bufferedReader.readLine())!=null){
    bufferedWriter.write(str);
    bufferedWriter.newLine();
}
bufferedReader.close();
bufferedWriter.close();
```

`copyFile(a,b)`使用String类型创建

`TransferTo()`:jdk10版本后新增

```java
reader.transferTo(writer);
```

