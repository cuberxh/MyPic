# 互联网数据传输原理 ｜OSI七层网络参考模型

## 物理层

把bit用不同的介质传输出去，数据从网络接口传输出去后会经过各种各样的网络拓扑，因此有集线器和中继器，

## 数据链路层 

定向数据发送的设备

把bit封装成帧（加入mac地址） ，

为了通过mac地址对不同的数据进行传输，就出现了交换机（二层交换机），交换机通过发送端和接受端的物理地址进行一跳一跳的传输。进行信息的差错检测、纠正、流控制避免传输和接受速度的不对称。

## 网络层

只用物理地址寻址，难以定位，需要IP地址进行寻址和路由选择。实现端到端传输的基础。路由器是网络层的核心。包是这一层的数据名字。路由器更具包里的地址进行转发，地址管理和路由选择就是这一层的核心。

## 传输层

对方主机可能运行了多个应用程序，用端口号来定位指定的程序，让数据去到指定的软件服务上。

实现服务进程到服务进程的传输，端就是传输层数据的名字。

传输层管理两个节点之间的传输，负责可靠传输（UDP）和不可靠传输（TCP） TCP允许把字节流分成多个段。

有流量控制保证传输速度，错误控制保证数据的完整接受。



## 会话层 数据名报文（应用数据）

保证用户状态和同步服务（cooicke? session?）数据名报文

## 表示层 数据名报文（应用数据）

会话层服务不同计算机表达的方式不一样表示层对其编码和解码

加密解密数据（HTTPS（SSL/TLS））

文件压缩

## 应用层	数据名报文（应用数据）

解决两个应用如何进行交互的问题

常见协议HTTP

<img src="E:\md笔记\image\image-20231118104843017.png" alt="image-20231118104843017" style="zoom:80%;" />





## 数据流通流程

<img src="E:\md笔记\image\image-20231118105422447.png" alt="image-20231118105422447" style="zoom: 67%;" />

### 应用层—网络层

目标IP和源IP不在同一网络下需要发送数据要经过默认网关

### 数据链路层

客户端需要在包中加入如自己和默认网关的MAC地址实现封装成帧，  实现跳到跳的传输

但是客户端并不知道，网关的MAC地址就需要ARP，获得默认网关的IP然后把包封装成帧

![image-20231118110251378](E:\md笔记\image\image-20231118110251378.png)

![image-20231118110345627](E:\md笔记\image\image-20231118110345627.png)

默认网关解封帧发现是发送给自己的，在解封包发现是另一网络的，进行路由转发，最终到达目的网络

<img src="E:\md笔记\image\image-20231118110724604.png" alt="image-20231118110724604" style="zoom: 67%;" />

到达目标网络对应的网关后如果知道目标MAC就直接发送，如果不知道就在ARP一次发送到目标主机

<img src="E:\md笔记\image\image-20231118110820064.png" alt="image-20231118110820064" style="zoom:67%;" />

目标主机收到到解封帧和包，发现是发送给自己的，解封段，查看目标端口到找到指定应用程序，应用程序处理好报文后根据源的信息作出响应。