---
layout: post

title: TCP/IP协议栈

categories:

- TCP/IP

tags:

- TCP/IP

---

##一、链路层解决问题

1. 接收和发送IP数据报
2. 接收和发送ARP请求
3. 接收和发送RARP请求

为什么要有time_wait状态：

a. 避免不同连接的数据混在一起
b. 可以重发最后一个fin包的ack

如何处理time_wait数量过多:

a. 让客户端关闭连接
b. 设置tcp_tw_reuse和tcp_tw_recycle参数

##二、 重传机制

### 2.1超时重传机制
### 2.2快速重传机制

### 2.3几种RTO的计算方法

超时重传时间：

* 设置太长，影响传输性能
* 设置太短，造成网络拥塞。

  经典算法：用加权移动平均法对rtt进行平滑处理：

   SRTT（平滑RTT） = (a*SRTT) + (1-a)*RTT
  (最近一次的rtt)
    RTO = min[UBOUND,max[LBOUND,b*SRTT]]

存在的问题：重传的时候用第一次的RTT还是重传的RTT

  * 没收到重传，重传的 RTT
  * 超时重传，第一次RTT

##  三、 流量控制
## 三、 TCP/IP拥塞处理

  为什么需要拥塞处理？
> 计算机网络中的路由器的缓存，链路，交换机在某个时间都是
> 有限的，为了避免在同一时间注入太多数据，导致链路和路由
> 器超过负载。


  相关概念
  * cwnd：拥塞窗口
  * ssthresh: 拥塞窗口的阀值

  拥塞处理机制：
  * 慢启动:cwnd<ssthresh
  * 拥塞避免: cwnd>=ssthresh
  * 拥塞状态: 发生重传(RTO超时或者三个相同ack)
  * 快速恢复: 连续三个相同ack   





（完）
