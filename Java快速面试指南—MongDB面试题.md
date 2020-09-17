# Contanct Me

如果觉得看起来比较麻烦，需要PDF版本，或是需要更多学习资料，都可以加上QQ群领取

>本群由我创立，目前已将群主权限交由合作方便于进行日常管理，介意的朋友们在GitHub上看最新版就好了
>
>> 这份笔记资料是会免费提供的，特地向你们保证…毕竟还是要恰饭的嘛…

祝愿每一位有追求的Java开发同胞都能进大厂拿高薪！

## QQ群

Java架构交流QQ群：**895538573**（备注一下GitHub，免得被认成打无良广告的）

快捷加群方式：[点击此处加入群聊【Java架构技术学习交流】：https://jq.qq.com/?_wv=1027&k=dYiE59DP

![](https://upload-images.jianshu.io/upload_images/22459064-6966a97afce07b87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



>PS：
>
>>平常很忙，找柚柚小姐姐领取就好了，免费获取的！

![](https://upload-images.jianshu.io/upload_images/22459064-088402b6d54b883f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

------



## 1\. 你说的NoSQL数据库是什么意思?NoSQL与RDBMS直接有什么区别?为什么要使用和不使用NoSQL数据库?说一说NoSQL数据库的几个优点?

NoSQL是非关系型数据库，NoSQL = Not Only SQL。

关系型数据库采用的结构化的数据，NoSQL采用的是键值对的方式存储数据。

在处理非结构化/半结构化的大数据时；在水平方向上进行扩展时；随时应对动态增加的数据项时可以优先考虑使用NoSQL数据库。

在考虑数据库的成熟度；支持；分析和商业智能；管理及专业性等问题时，应优先考虑关系型数据库。

## 2\. NoSQL数据库有哪些类型?

[NoSQL数据库的类型](http://theprofessionalspoint.blogspot.in/2014/01/types-and-examples-of-nosql-databases.html)

例如：MongoDB, Cassandra, CouchDB, Hypertable, Redis, Riak, Neo4j, HBASE, Couchbase, MemcacheDB, RevenDB and Voldemort are the examples of NoSQL databases.[详细阅读](http://theprofessionalspoint.blogspot.in/2014/01/12-best-free-and-open-source-nosql.html)。

## 3\. MySQL与MongoDB之间最基本的差别是什么?

MySQL和MongoDB两者都是免费开源的数据库。MySQL和MongoDB有许多基本差别包括数据的表示(data representation)，查询，关系，事务，schema的设计和定义，标准化(normalization)，速度和性能。

通过比较MySQL和MongoDB，实际上我们是在比较关系型和非关系型数据库，即数据存储结构不同。[详细阅读](http://theprofessionalspoint.blogspot.in/2013/12/mysql-vs-mongodb-basic-differences.html)

## 4\. 你怎么比较MongoDB、CouchDB及CouchBase?

MongoDB和CouchDB都是面向文档的数据库。MongoDB和CouchDB都是开源NoSQL数据库的最典型代表。 除了都以文档形式存储外它们没有其他的共同点。MongoDB和CouchDB在数据模型实现、接口、对象存储以及复制方法等方面有很多不同。

细节可以参见下面的链接：

[MongDB vs CouchDB](http://theprofessionalspoint.blogspot.in/2014/01/couchdb-vs-couchbase-differences-and.html)

[CouchDB vs CouchBase](http://theprofessionalspoint.blogspot.in/2014/01/couchdb-vs-couchbase-differences-and.html)

## 5\. MongoDB成为最好NoSQL数据库的原因是什么?

以下特点使得MongoDB成为最好的NoSQL数据库：

· 面向文件的

· 高性能

· 高可用性

· 易扩展性

· 丰富的查询语言

## 6.32位系统上有什么细微差别?

journaling会激活额外的内存映射文件。这将进一步抑制32位版本上的数据库大小。因此，现在journaling在32位系统上默认是禁用的。

## 7\. journal回放在条目(entry)不完整时(比如恰巧有一个中途故障了)会遇到问题吗?

每个journal (group)的写操作都是一致的，除非它是完整的否则在恢复过程中它不会回放。

## 8\. 分析器在MongoDB中的作用是什么?

MongoDB中包括了一个可以显示数据库中每个操作性能特点的数据库分析器。通过这个分析器你可以找到比预期慢的查询(或写操作);利用这一信息，比如，可以确定是否需要添加索引。

## 9\. 名字空间(namespace)是什么?

MongoDB存储BSON对象在丛集(collection)中。数据库名字和丛集名字以句点连结起来叫做名字空间(namespace)。

## 10\. 如果用户移除对象的属性，该属性是否从存储层中删除?

是的，用户移除属性然后对象会重新保存(re-save())。

## 11\. 能否使用日志特征进行安全备份?

是的。

## 12\. 允许空值null吗?

对于对象成员而言，是的。然而用户不能够添加空值(null)到数据库丛集(collection)因为空值不是对象。然而用户能够添加空对象{}。

## 13\. 更新操作立刻fsync到磁盘?

不会，磁盘写操作默认是延迟执行的。写操作可能在两三秒(默认在60秒内)后到达磁盘。例如，如果一秒内数据库收到一千个对一个对象递增的操作，仅刷新磁盘一次。(注意，尽管fsync选项在命令行和经过getLastError_old是有效的)(译者：也许是坑人的面试题??)。

## 14\. 如何执行事务/加锁?

MongoDB没有使用传统的锁或者复杂的带回滚的事务，因为它设计的宗旨是轻量，快速以及可预计的高性能。可以把它类比成MySQL MylSAM的自动提交模式。通过精简对事务的支持，性能得到了提升，特别是在一个可能会穿过多个服务器的系统里。

## 15\. 为什么我的数据文件如此庞大?

MongoDB会积极的预分配预留空间来防止文件系统碎片。

## 16\. 启用备份故障恢复需要多久?

从备份数据库声明主数据库宕机到选出一个备份数据库作为新的主数据库将花费10到30秒时间。这期间在主数据库上的操作将会失败--包括写入和强一致性读取(strong consistent read)操作。然而，你还能在第二数据库上执行最终一致性查询(eventually consistent query)(在slaveOk模式下)，即使在这段时间里。

## 17\. 什么是master或primary?

## 18\. 什么是secondary或slave?

## 19\. 我必须调用getLastError来确保写操作生效了么?

## 20\. 我应该启动一个集群分片(sharded)还是一个非集群分片的 MongoDB 环境?

## 21\. 分片(sharding)和复制(replication)是怎样工作的?

## 22\. 数据在什么时候才会扩展到多个分片(shard)里?

## 23\. 当我试图更新一个正在被迁移的块(chunk)上的文档时会发生什么?

## 25\. 我可以把moveChunk目录里的旧文件删除吗?

## 26\. 我怎么查看 Mongo 正在使用的链接?

## 27\. 如果块移动操作(moveChunk)失败了，我需要手动清除部分转移的文档吗?

## 28\. 如果我在使用复制技术(replication)，可以一部分使用日志(journaling)而其他部分则不使用吗?

## 29.当更新一个正在被迁移的块（Chunk）上的文档时会发生什么？

## 30.MongoDB在A:{B,C}上建立索引，查询A:{B,C}和A:{C,B}都会使用索引吗？

## 31.如果一个分片（Shard）停止或很慢的时候，发起一个查询会怎样？

## 32\. MongoDB支持存储过程吗？如果支持的话，怎么用？

## 33.如何理解MongoDB中的GridFS机制，MongoDB为何使用GridFS来存储文件？

# **欢迎关注我的B站：**https://space.bilibili.com/294387431

