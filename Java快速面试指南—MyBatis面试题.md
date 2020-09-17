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

## 1、什么是Mybatis？

> 1.Mybatis是一个半ORM（对象关系映射）框架，它内部封装了JDBC，开发时只需要关注SQL语句本身，不需要花费精力去处理加载驱动、创建连接、创建statement等繁杂的过程。程序员直接编写原生态sql，可以严格控制sql执行性能，灵活度高。
> 
> 2.MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO映射成数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。
> 
> 3.通过xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过java对象和 statement中sql的动态参数进行映射生成最终执行的sql语句，最后由mybatis框架执行sql并将结果映射为java对象并返回。（从执行sql到返回result的过程）。

## **2、Mybaits的优点：**

> 1.基于SQL语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响，SQL写在XML里，解除sql与程序代码的耦合，便于统一管理；提供XML标签，支持编写动态SQL语句，并可重用。
> 
> 2.与JDBC相比，减少了50%以上的代码量，消除了JDBC大量冗余的代码，不需要手动开关连接；
> 
> 3.很好的与各种数据库兼容（因为MyBatis使用JDBC来连接数据库，所以只要JDBC支持的数据库MyBatis都支持）。
> 
> 4.能够与Spring很好的集成；
> 
> 5.提供映射标签，支持对象与数据库的ORM字段关系映射；提供对象关系映射标签，支持对象关系组件维护。

## **3.MyBatis框架的缺点：**

> 1.SQL语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写SQL语句的功底有一定要求。
> 
> 2.SQL语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。

## **4、MyBatis框架适用场合：**

> 1.MyBatis专注于SQL本身，是一个足够灵活的DAO层解决方案。
> 
> 2.对性能的要求很高，或者需求变化较多的项目，如互联网项目，MyBatis将是不错的选择。

## **5、MyBatis与Hibernate有哪些不同？**

> 1.Mybatis和hibernate不同，它不完全是一个ORM框架，因为MyBatis需要程序员自己编写Sql语句。
> 
> 2.Mybatis直接编写原生态sql，可以严格控制sql执行性能，灵活度高，非常适合对关系数据模型要求不高的软件开发，因为这类软件需求变化频繁，一但需求变化要求迅速输出成果。但是灵活的前提是mybatis无法做到数据库无关性，如果需要实现支持多种数据库的软件，则需要自定义多套sql映射文件，工作量大。
> 
> 3.Hibernate对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件，如果用hibernate开发可以节省很多代码，提高效率。

## **6、#{}和${}的区别是什么？**

>  {}是预编译处理，${}是字符串替换。
> 
> Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；
> 
> Mybatis在处理${}时，就是把${}替换成变量的值。
> 
> 使用#{}可以有效的防止SQL注入，提高系统安全性。

##**7、当实体类中的属性名和表中的字段名不一样 ，怎么办 ？**

第1种： 通过在查询的sql语句中定义字段名的别名，让字段名的别名和实体类的属性名一致。

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-809626bd6a539e0c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

第2种： 通过 <resultMap>来映射字段名和实体类属性名的一一对应的关系。

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-56a2dfdc7fde0de4?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

## **8、 模糊查询like语句该怎么写?**

第1种：在Java代码中添加sql通配符。

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-2a758f3f971c91d0?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

第2种：在sql语句中拼接通配符，会引起sql注入

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-31af7772855eb28d?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

## **9、通常一个Xml映射文件，都会写一个Dao接口与之对应，请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？**

> Dao接口即Mapper接口。接口的全限名，就是映射文件中的namespace的值；接口的方法名，就是映射文件中Mapper的Statement的id值；接口方法内的参数，就是传递给sql的参数。
> 
> Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MapperStatement。在Mybatis中，每一个 **、、、**标签，都会被解析为一个MapperStatement对象。
> 
> 举例： **com.mybatis3.mappers.StudentDao.findStudentById**，可以唯一找到namespace为 **com.mybatis3.mappers.StudentDao**下面 id 为 findStudentById 的 MapperStatement。
> 
> Mapper接口里的方法，是不能重载的，因为是使用 全限名+方法名 的保存和寻找策略。Mapper 接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Mapper接口生成代理对象proxy，代理对象会拦截接口方法，转而执行MapperStatement所代表的sql，然后将sql执行结果返回。

## **10、Mybatis是如何进行分页的？分页插件的原理是什么？**

> Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页。可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。
> 
> 分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据dialect方言，添加对应的物理分页语句和物理分页参数。

## **11、Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？**

> 第一种是使用 <resultMap>标签，逐一定义数据库列名和对象属性名之间的映射关系。
> 
> 第二种是使用sql列的别名功能，将列的别名书写为对象属性名。
> 
> 有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。

## **12、如何执行批量插入?**

首先,创建一个简单的insert语句:

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-415ec7b4a6ac80d6?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

然后在java代码中像下面这样执行批处理插入:

![24道Mybatis常见面试题总结及答案！](https://upload-images.jianshu.io/upload_images/11474088-9cc56016e24a00dd?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 

## **13、如何获取自动生成的(主)键值?**

## **14、Mybatis动态sql有什么用？执行原理？有哪些动态sql？**

## **15、Xml映射文件中，除了常见的select|insert|updae|delete标签之外，还有哪些标签？**

## **16、Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？**

## **17、为什么说Mybatis是半自动ORM映射工具？它与全自动的区别在哪里？**

## **18、MyBatis实现一对一有几种方式?具体怎么操作的？**

## **19、MyBatis实现一对多有几种方式,怎么操作的？**

## **20、Mybatis是否支持延迟加载？如果支持，它的实现原理是什么？**

## **21、Mybatis的一级、二级缓存:**

## **22、什么是MyBatis的接口绑定？有哪些实现方式？**

## **23、使用MyBatis的mapper接口调用时有哪些要求？**

## **24、简述Mybatis的插件运行原理，以及如何编写一个插件。**

**欢迎关注我的B站：**https://space.bilibili.com/294387431