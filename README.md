# IM_Project-
此项目为大二上学期期末实训项目，个人根据网上的例子，完善的即时通讯项目，相当于对自己所学的Java进行实战运用

全年寒假开始接触JAVA，到现在已经快一年了，但是真正去学JAVA的时间只有3个月左右，其他时间都去做Android去了，之前就一直想用JAVA去做一些小Demo，感觉很有意思，但是，一直不知道如何下手，特别是socket这一块，Android中，目前都没怎么接触，所以借这次实训，想好好的用JAVA做点东西出来
### 一、功能介绍
先说一下这个项目实现了的功能：
1. 聊天室功能：群聊、私聊
2. 文件共享
3. 好友在线列表、在线人数
4. 换聊天背景功能
#### 二、项目中各个类的功能及使用问题
1. `Main`：
项目的开始位置，里面有一个swing的工作线程，但是并未真正去实现
##### 客户端：
2. `ChatClient`封装客户端与服务器通信的细节
项目就是从这里去连接服务器，并且将IO流与socket绑定，同时实现了对不同事务的处理方法
3. `ChatClientThread`客户端消息线程，用以接收服务器消息
客户端在这里监听服务器的消息，先将IO流中的数据解析，再根据协议去对不同消息类型进行处理(如登录，群聊，私聊，用户列表刷新类型消息等)
4. `GroupChatView`聊天视图(swing实现)
用于构建用户聊天窗口，并将线程里面处理后的数据展示到界面上
【注】根据自己服务器的类型，进行代码更改：
```
        // 连接服务器
		client.conn("云服务器IP", 8989);
		//如果是用自己的电脑作为服务器，就将IP设为127.0.0.1
//		client.conn("127.0.0.1", 8989);
```
![项目界面](https://upload-images.jianshu.io/upload_images/15748212-6be65434d0c7e8af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
5. `GroupFileView`文件传输窗口
用于展示共享文件，可供用户上传和下载，以及刷新
【注】IP地址根据自己的服务器类型进行选择
```
    private String ip = "云服务器IP";//服务器地址
    //如果是用自己的电脑作为服务器，就将IP设为127.0.0.1
//		client.conn("127.0.0.1", 8989);
```
![文件视图](https://upload-images.jianshu.io/upload_images/15748212-9c3b6b9abf4edf65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 服务端：
6. `ChatServer`聊天服务器类
负责接受客户端的连接，将客户端的连接交付给服务器端线程处理，是聊天服务端的开始地方
7. `ChatServerThread`聊天服务器端线程
负责与客户端通信，与客户端线程一样，用于监听消息，并通过工具类对其解析，然后根据消息类型进行处理，同时，这个类中有对异常的捕获，使服务端的健壮性增强
8. `FileServer`文件服务器(文件服务器的线程`ServerThread`类放在内部)
用于监听客户端的文件发送和下载，并对其进行处理，这里也是文件服务端的开始
```
    //服务端的文件存储路径(此为云服务器上的地址)
    private String path ="C:\\Users\\Administrator\\Desktop\\jar\\file";
    //也可以将共享文件存到这个项目的路径下
//    private String path ="file";
```
9. `UserInfo`将用户和他对应的DataOutputSteam进行抽象形成的类，方便user和其使用的IO流进行绑定
##### 工具类：
10. `ChatProtocol`协议工具类
封装了消息的类型以及发和收的方法，能发送数据到数据流中，也能将数据流中的数据进行解析
11. `ChatResult`封装一个消息，亦是一次解析的结果
将消息类型，长度，和数据合并成一个对象，在数据流上面传输
12. `ParseDataUtil`规定文件的发送和处理格式，便于对用户上传和下载的文件进行封装和解析

###简书地址：https://www.jianshu.com/p/f23332a9a8bf




