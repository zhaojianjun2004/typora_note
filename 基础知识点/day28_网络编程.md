day28

### 一.网络基础

#### 1.七层：

比如玩网络游戏

第一层：物理层：要有（网卡）、网线

第二层：数据链路层：要有能访问服务器的工具，mac地址、（交换机）

第三层：网络层：要有（路由器）（实现不同网络之间的路径选择）

第四层：传输层：访问的协议和端口号（防火墙）

第五层：会话层：可以和服务器进行网络连接

第六层：表示层：向服务器发送指令，对指令进行二进制翻译，然后压缩、传到服务器

第七层：应用层：界面展示（计算机）

#### 2.TCP/IP协议：

（传输控制协议/网际协议），在多个不同的网络间实现信息传输的协议族

是一个四层的体系结构：应用层、传输层、网络层和物理+数据链路层





### 二.网络编程

#### 1.三要素：

协议、IP地址、端口号

- （IP地址）确定接受的对象，设备在网络中的地址是唯一的标识

> IPv4：互联网通信协议第四版，采用32位地址长度，分成4组，每一组8位，所以0-255，例如（192.168.1.66）,2^32个IP
>
> IPv6：第6版，采用128比特位，分成8组，2^128个IP，

> <!--常用的CMD命令：-->
>
> ipconfig:查看本机ip地址
>
> ping:检查网络是否连通

- （端口号）确定接受数据的软件，是应用程序在设备中唯一的标识，

- （协议）确定网络传输的规则，常见的协议有UDP、TCP、https、ftp

> <!--关于协议的小知识-->
>
> 应用层：HTTP、FTP、DNS...
>
> 传输层：TCP（<span style="color:red;">面向连接</span>通信协议,数据安全）、UDP(用户数据报协议，是<span style="color:red;">面向无连接</span>通信协议,数据不安全)...
>
> 网络层：IP、ICMP、ARP...
>
> 物理链路层：硬件设备01010101...

#### 2.网络开发模式：

##### C/S结构：客户端/服务器模式

##### B/S结构：浏览器/服务器模式



#### 3.Socket套接字

##### 3.1 简介

使用socket套接字来实现两个程序间的双向通信，通讯的两端都有socket，数据在socket之间使用IO传输



##### 3.2基于TCP的Socket编程

###### 3.2.1  实现聊天服务

> Clinet端（客户端）

- 首先实例化Socket来连接到主机和端口（两个参数）；

- 然后使用输入输出流来发送和接收数据，从套接字中获取输出流，使用`PrintWriter`来向服务器发送消息，同时从套接字获取输入流`InputStream`，创建`InputStreamReader`对象来将输入流中的字节转换为字符，并使用`BufferedReader`来读取服务器发送的消息（包装`InputStreamReader`）

- 然后使用`Scanner`读取用户输入，使用`PrintWriter`类来向服务器发送信息，PrintWriter还提供了`flush()`方法来确保发送成功

- 然后就是根据判定来获取输入，以及什么情况退出循环并关闭连接`break`



> 服务器端：

- 





##### 3.3基于UDP的Socket编程

```java
//发送数据
//1.创建DatagramSocket对象
//细节：绑定端口（以后我们就通过这个端口往外发送），有参就是指定端口绑定
DatagramSocket ds= new DatagramSocket();

//2.打包数据
String msg="有内鬼停止交易";
byte[] bytes=msg.getBytes(StandardCharsets.UTF-8);
int port=10086;
InetAddress address=InetAddress.getByName("122.0.0.1");
DatagramPocket packet=new DatagramPacket(bytes,bytes.length,address,port);//四个参数

//3.发送数据
ds.send(packet);

//4.释放资源
ds.close();

```

```java
//接收数据
//形象理解为取快递：
//1.创建接收端的DatagramSocket对象（找快递公司）
//细节：接收的时候一定要绑定端口，且要和发送的端口保持一致
DatagramSocket ds=new DatagramSocket(10086);

//2.接收打包好的数据（接收箱子）
byte[]bytes=new byte[1024];
DatagramPacket dp=new DatagramPacket(bytes,bytes.length);
ds.receive(dp);
//3.解析数据包（从箱子里面拿出礼物）
byte[] data=dp.getData();
int len=dp.getLength();
InetAddress address=dp.getAddress();
int port=dp.getPort();
//4，释放资源（签收走人）

```

​	