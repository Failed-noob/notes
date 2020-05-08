### **http 协议 **

协议的定义:  ，网络协议的简称，网络协议是通信计算机双方必须共同遵从的一组约定。如怎么样建立连接、怎么样互相识别等。只有遵守这个约定，计算机之间才能相互通信交流。它的三要素是：语法、语义、时序。为了使数据在网络上从源到达目的，网络通信的参与方必须遵循相同的规则，这套规则称为协议（protocol）



**　**http协议是基于TCP/IP协议之上的应用层协议。****



**http [ HyperText transfer protocol ]  超文本传输协议;**

是一种用于分布式,协作式和超媒体信息系统应用层协议 ; HTTP是万维网的数据通信的基础;



**http 请求 / 响应的步骤例子 [当然之间有很多细节 下面就来尽量详细解释]:**

1. 在浏览器地址栏中输入 url    浏览器回想DNS服务器请求解析的域名所对应的IP地址;
2. 解析出ip地址后,根据IP地址和端口,和服务器简历TCP连接
3. 浏览器发出读取文件 的http请求,该请求报文作为TCP 三次握手的第三个报文的数据发送给服务器;
4. 服务器作出响应,并将对应的html 发送给浏览器
5. 释放TCP连接
6. 浏览器显示内容



![](D:\QQ截图\三次握手四次挥手.gif)

//这里只能是简洁的介绍 下面的概念 

DNS 服务器 : [ Nomain  Name system]  它是由解析器以及域名服务器组成的。域名服务器是指保存有该网络中所有主机的域名和对应IP地址，并具有将域名转换为IP地址功能的服务器 [ **域名是指向 ip的 ,域名是给看的,IP是计算机之间能够读懂的** ];



------

TCP 连接:  (在这里先简要了解一下 TCP [ transmission control protocol ] 传输控

制协议 是一种面向连接的、可靠的、基于字节流的传输层通信协议);

TCP连接 通过三次握手建立连接;

**首先Client端发送连接请求报文，Server段接受连接后回复ACK报文，并为这次连接分配资源。Client端接收到ACK报文后也向Server段发生ACK报文，并分配资源，这样TCP连接就建立了。**



{	

​	//这里稍微带一下 断开连接过程是怎么样的;

​	//**当client 发起中断请求时** client 发送 <u>FIN报文</u> 给server 此时client会通知server client没有数据要发送了,但若你还有数据没有发送完成,则不必关闭socket,可以继续发送; 然后 server 会发送一个ACK  这时候client 会认为 server 还没准备好 然后继续等待;此时client 就进入一个 FIN_WAIT [ 等待完成状态 ] 然后继续等待 server端的 FIN报文

​	//**当server 发起中断请求时**

当Server端确定数据已发送完成，则向Client端发送FIN报文，"告诉Client端，好了，我这边数据发完了，准备好关闭连接了"。Client端收到FIN报文后，"就知道可以关闭连接了，但是他还是不相信网络，怕Server端不知道要关闭，所以发送ACK后进入TIME_WAIT状态，如果Server端没有收到ACK则可以重传。“，Server端收到ACK后，"就知道可以断开连接了"。Client端等待了2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，我Client端也可以关闭连接了

}





*Ack*nowledge character [确认字符]        SYN [**Synchronize Sequence Numbers**]  同步序列编号

------

四次挥手

第一次挥手:
Client将FIN置为1,序号seq=M,发送给Server,进入FIN_WAIT_1状态

第二次挥手
Server收到后,将ACK置为1,ack=M+1,响应给Client,进入CLOSE_WAIT状态
Client收到响应后,进入FIN_WAIT_2状态


第三次挥手
Server在结束所有数据传输后,将Fin置为1,seq=N+1,发送给Client,进入
LAST_ACK状态


第四次挥手
Client收到后,将ACK置为1,ack=N+1,响应给Server,进入TIME_WAIT状态,等待
​    2MSL后,进入CLOSED状态
Server收到后,进入CLOSED状态



