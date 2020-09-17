[TOC]

------

注意一下咯：更多关于Java集合、JVM、多线程并发、spring原理、微服务、Netty 与RPC 、Kafka、日记、设计模式、Java算法、数据库、Zookeeper、分布式缓存、数据结构等等**加QQ群：895538573 管理员处可免费获取！**

------



# 基础篇

## 1、TCP、UDP的区别？

TCP与UDP区别总结：

1)、TCP面向连接（如打电话要先拨号建立连接）;UDP是无连接的，即发送数据之前不需要建立连接。

2)、TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保证可靠交付

3)、TCP面向字节流，实际上是TCP把数据看成一连串无结构的字节流;UDP是面向报文的
UDP没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如IP电话，实时视频会议等）

4)、每一条TCP连接只能是点到点的;UDP支持一对一，一对多，多对一和多对多的交互通信

5)、TCP首部开销20字节;UDP的首部开销小，只有8个字节

6)、TCP的逻辑通信信道是全双工的可靠信道，UDP则是不可靠信道

## 2、TCP协议如何保证可靠传输？

https://www.cnblogs.com/xiaokang01/p/10033267.html

## 3、TCP的握手、挥手机制？

TCP的握手机制：

![img](file:///C:\Users\XXTG\AppData\Local\Temp\ksohtml13924\wps1.png) 

TCP的挥手机制：

![img](file:///C:\Users\XXTG\AppData\Local\Temp\ksohtml13924\wps2.png) 

详情参考文章：
https://blog.csdn.net/qzcsu/article/details/72861891

## 4、TCP的粘包/拆包原因及其解决方法是什么？

为什么会发生TCP粘包、拆包？
 发生TCP粘包、拆包主要是由于下面一些原因： 

1).应用程序写入的数据大于套接字缓冲区大小，这将会发生拆包。

2).应用程序写入数据小于套接字缓冲区大小，网卡将应用多次写入的数据发送到网络上，这将会发生粘包。

3).进行MSS（最大报文长度）大小的TCP分段，当TCP报文长度-TCP头部长度>MSS的时候将发生拆包。

4).接收方法不及时读取套接字缓冲区数据，这将发生粘包。

 粘包、拆包解决办法: 

TCP本身是面向流的，作为网络服务器，如何从这源源不断涌来的数据流中拆分出或者合并出有意义的信息呢？通常会有以下一些常用的方法：

1)、发送端给每个数据包添加包首部，首部中应该至少包含数据包的长度，这样接收端在接收到数据后，通过读取包首部的长度字段，便知道每一个数据包的实际长度了。

2)、发送端将每个数据包封装为固定长度（不够的可以通过补0填充），这样接收端每次从接收缓冲区中读取固定长度的数据就自然而然的把每个数据包拆分开来。

3)、可以在数据包之间设置边界，如添加特殊符号，这样，接收端通过这个边界就可以将不同的数据包拆分开。

详情参考文章：[https://www.cnblogs.com/panch...](https://www.cnblogs.com/panchanggui/p/9518735.html)

##  5、Netty的粘包/拆包是怎么处理的，有哪些实现？ 

 对于粘包和拆包问题，常见的解决方案有四种： 

1)、客户端在发送数据包的时候，每个包都固定长度，比如1024个字节大小，如果客户端发送的数据长度不足1024个字节，则通过补充空格的方式补全到指定长度；Netty提供的FixedLengthFrameDecoder

2)、客户端在每个包的末尾使用固定的分隔符，例如rn，如果一个包被拆分了，则等待下一个包发送过来之后找到其中的rn，然后对其拆分后的头部部分与前一个包的剩余部分进行合并，这样就得到了一个完整的包；Netty提供LineBasedFrameDecoder与DelimiterBasedFrameDecoder

3)、将消息分为头部和消息体，在头部中保存有当前整个消息的长度，只有在读取到足够长度的消息之后才算是读到了一个完整的消息；Netyy提供了LengthFieldBasedFrameDecoder与LengthFieldPrepender

4)、通过自定义协议进行粘包和拆包的处理。Netty提供了通过实现MessageToByteEncoder和ByteToMessageDecoder来实现

更详细请阅读文章：[https://www.cnblogs.com/AIPAO...](https://www.cnblogs.com/AIPAOJIAO/p/10631551.html)

##  6、同步与异步、阻塞与非阻塞的区别？ 

简单点理解就是：

1). 同步，就是我调用一个功能，该功能没有结束前，我死等结果。

2). 异步，就是我调用一个功能，不需要知道该功能结果，该功能有结果后通知我（回调通知）

3). 阻塞，就是调用我（函数），我（函数）没有接收完数据或者没有得到结果之前，我不会返回。

4). 非阻塞，就是调用我（函数），我（函数）立即返回，通过select通知调用者

同步IO和异步IO的区别就在于：数据拷贝的时候进程是否阻塞

阻塞IO和非阻塞IO的区别就在于：应用程序的调用是否立即返回

##  7、说说网络IO模型？ 

![img](file:///C:\Users\XXTG\AppData\Local\Temp\ksohtml13924\wps3.jpg) 

##  8、BIO、NIO、AIO分别是什么？ 

 BIO:同步并阻塞 ，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善。BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解。

 NIO:同步非阻塞 ，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持。

 AIO:异步非阻塞 ，服务器实现模式为一个有效请求一个线程，客户端的I/O请求都是由OS先完成了再通知服务器应用去启动线程进行处理.AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持。

##  9、select、poll、epoll的机制及其区别？ 

1).单个进程打开的文件描述符（fd文件句柄）不一致

select ：有最大连接数限制数为1024，单个进程所能打开的最大连接数由FD_ZETSIZE宏定义。

poll：poll本质上与select没有区别，但是它没有最大连接数的限制，原因是它是基于链表来存储的。

epoll：虽然连接有上限，但是很大，1G内存的机器可以打开10万左右的连接，以此类推。

2).监听Socket的方式不一致

select ：轮询的方式，一个一个的socket检查过去，发现有socket活跃时才进行处理，当线性socket增多时，轮询的速度将会变得很慢，造成线性造成性能下降问题。

poll：对select稍微进行了优化，只是修改了文件描述符，但是监听socket的方式还是轮询。

expoll：epoll内核中实现是根据每个fd上的callback函数来实现的，只有活跃的socket才会主动调用callback，通知expoll来处理这个socket。（会将连接的socket注册到epoll中, 相当于socket的花名册, 如果有一个socket活跃了, 会回调一个函数, 通知epoll,赶紧过来处理）

3).内存空间拷贝方式（消息传递方式）不一致

select：内核想将消息传递到用户态，需要将数据从内核态拷贝到用户态,这个过程非常的耗时

poll：同上

epoll：epoll的内核和用户空间共享一块内存，因此内存态数据和用户态数据是共享的

select、poll、epoll时间复杂度分别是：O(n)、O(n)、O(1)

##  10、说说你对Netty的了解？ 

这个没用过的话，就不要死撑了。用过的估计不用找了吧。

##  11、Netty跟Java NIO有什么不同，为什么不直接使用JDK NIO类库？ 

##  12、Netty组件有哪些，分别有什么关联？ 

##  13、说说Netty的执行流程？ 

#  高级篇 

##  14、Netty高性能体现在哪些方面？ 

[https://www.infoq.cn/article/...](#theCommentsSection)

##  15、Netty的线程模型是怎么样的？ 

##  16、Netty的零拷贝提体现在哪里，与操作系统上的有什么区别？ 

##  17、Netty的内存池是怎么实现的？ 

netty内存池实现原理

netty内存池可以分配堆内存和非堆内存（Direct内存），内存分配的核心算法是类似的，从堆内存分配代码入手来学习整个内存池的原理。netty框架处理IO事件时，使用ByteBuf承载数据。ByteBuf的内存分配由PooledByteBufAllocator来执行，最终的内存分配工作会被委托给PoolArena，堆内存分配的PoolArena实现是HeapArena。

netty通常被用于高并发系统，多线程竞争加锁会影响内存分配的效率，为了缓解高并发时的线程竞争，netty允许使用者创建多个分配器（PoolArena）来分离线程竞争，提高内存分配效率。可通过PooledByteBufAllocator构造子中的nHeapArena参数来设置PoolArena的数量，或者直接取框架中的默认值，通过以下代码决定默认值，默认值根据CPU核心数、JVM最大可用内存以及默认内存块（PoolChunk）大小等参数来计算这个默认值，计算逻辑是：

1）获取系统变量io.netty.allocator.numHeapArenas，通过System.setProperty("io.netty.allocator.numHeapArenas",xxx)或者增加JVM启动参数-Dio.netty.allocator.numHeapArenas=xxx设置，如果设置了值，把这个值当做Arena的个数。

2）如果没有设置io.netty.allocator.numHeapArenas系统变量，计算CPU核心数*2和JVM最大可用内存/默认内存块大小/2/3，取其中一个较少的值当做PoolArena的个数。

确定PoolArena个数之后框架会创建一个PoolArena数组，数组中所有的PoolArena都会用来执行内存分配。线程申请内存分配时，线程会在这个PoolArena数组中挑选一个当前被占用次数最少的Arena执行内存分配。

此外，netty使用扩展的线程对象FastThreadLocalThread来优化ThreadLocal性能，具体的优化思路是：默认的ThreadLocal使用ThreadLocalMap存储线程局部变量，它的实现方式类似于HashMap，需要计算hashCode定位到线程局部变量所在Entry的索引，而FastThreadLocalThread使用FastThreadLocal代替ThreadLocal，FastThreadLocalThread用一个数组来维护线程变量，每个FastThreadLocal维护一个index，该index就是线程局部变量在数组中的位置，线程变量直接通过index访问无需计算hashCode，FastThreadLocal的优势是减少了hashCode的计算过程，虽然性能只会有轻微的提升，但在高并发系统中，即使只是轻微的提升也会成倍放大。

更多请阅读文章：[http://baijiahao.baidu.com/s?...](http://baijiahao.baidu.com/s?id=1640499946352354049&wfr=spider&for=pc)

##  18、Netty的对象池是怎么实现的？ 

Netty 并没有使用第三方库实现对象池，而是自己实现了一个相对轻量的对象池。通过使用 threadLocal，避免了多线程下取数据时可能出现的线程安全问题，同时，为了实现多线程回收同一个实例，让每个线程对应一个队列，队列链接在 Stack 对象上形成链表，这样，就解决了多线程回收时的安全问题。同时，使用了软引用的map 和 软引用的 thradl 也避免了内存泄漏。

![img](file:///C:\Users\XXTG\AppData\Local\Temp\ksohtml13924\wps9.jpg) 

更详细的可阅读文章：

[https://www.jianshu.com/p/834...](https://www.jianshu.com/p/83469191509b)
[https://www.cnblogs.com/hzmar...](https://www.cnblogs.com/hzmark/p/netty-object-pool.html)

 

#  实战篇 

##  19、在实际项目中，你们是怎么使用Netty的？ 

##  20、使用过Netty遇到过什么问题？ 

##  21、netty的线程模型，netty如何基于reactor模型上实现的。 

[https://www.cnblogs.com/codin...](https://www.cnblogs.com/coding400/p/10865333.html)

![img](file:///C:\Users\XXTG\AppData\Local\Temp\ksohtml13924\wps11.jpg) 

##  2  2  、netty的fashwheeltimer的用法，实现原理，是否出现过调用不够准时，怎么解决。 

[https://www.cnblogs.com/eryua...](https://www.cnblogs.com/eryuan/p/7955677.html)

##  2  3  、netty的心跳处理在弱网下怎么办。 

[https://blog.csdn.net/z691837...](https://blog.csdn.net/z69183787/article/details/52671543)

##  2  4  、netty的通讯协议是什么样的。 

[https://www.cnblogs.com/54929...](https://www.cnblogs.com/549294286/p/11241357.html)