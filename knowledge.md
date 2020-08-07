# JAVA

## java基础

### 集合

![image-20200730135335826](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200730135335826.png)

#### List

有序的collection，主要有三个实现类分别为ArrayList，Vector，LinkedList

##### ArrayList

**基于数组实现，增删慢，查询快，线程不安全**

基于数组实现，提供了add、remove、get功能

缺点：对元素必须连续存储，当需要在ArrayList的中间位置增减元素时，会造成周围元素的的移动，修改代价很高，因此ArrayList不适合做随机的的插入和删除操作，更适合随机的查找和遍历

ArrayList不需要在定义的时候指定长度，在数组长度不符合存储要求的时候Arraylist会创建一个更大的数组并将数组中已有的数据复制到新的数组中

##### Vector

**基于数组实现，增删慢，查询快，线程安全**

Vector的数据结构和ArrayList一样，都是基于数组实现的，不同的是Vector支持线程同步，即同一时刻只允许一个线程对Vector进行写操作（新增、删除、修改），以保证多线程环境下数据的一致性，但需要频繁地对Vector实例进行加锁和释放锁操作，因此，Vector的读写效率在整体上比ArrayList低。

##### **LinkedList**

**基于双向链表实现，增删快，查询慢，线程不安全**

LinkedList采用双向链表结构存储元素，在对LinkedList进行插入和删除操作时，只需在对应的节点上插入或删除元素，并将上一个节点元素的下一个节点的指针指向该节点即可，数据改动较小，因此随机插入和删除效率很高。但在对LinkedList进行随机访问时，需要从链表头部一直遍历到该节点为止，因此随机访问速度很慢。除此之外，LinkedList还提供了在List接口中未定义的方法，用于操作链表头部和尾部的元素，因此有时可以被当作堆栈、队列或双向队列使用。

#### SET

Set核心是独一无二的性质，适用于存储无序且值不相等的元素。对象的相等性在本质上是对象的HashCode值相同，Java依据对象的内存地址计算出对象的HashCode值。如果想要比较两个对象是否相等，则必须同时覆盖对象的hashCode方法和equals方法，并且hashCode方法和equals方法的返回值必须相同。

##### HashSet

**HashTable实现，无序**

HashSet存放的是散列值，它是按照元素的散列值来存取元素的。元素的散列值是通过元素的hashCode方法计算得到的，HashSet首先判断两个元素的散列值是否相等，如果散列值相等，则接着通过equals方法比较，如果equls方法返回的结果也为true，HashSet就将其视为同一个元素；如果equals方法返回的结果为false，HashSet就不将其视为同一个元素。

##### TreeSet

**二叉树实现**

TreeSet基于二叉树的原理对新添加的对象按照指定的顺序排序（升序、降序），每添加一个对象都会进行排序，并将对象插入二叉树指定的位置。
Integer和String等基础对象类型可以直接根据TreeSet的默认排序进行存储，而自定义的数据类型必须实现Comparable接口，并且覆写其中的compareTo函数才可以按照预定义的顺序存储。若覆写compare函数，则在升序时在this.对象小于指定对象的条件下返回-1，在降序时在this.对象大于指定对象的条件下返回1。

##### LinkHashSet

HashTable实现数据存储，双向链表记录顺序

LinkedHashSet在底层使用LinkedHashMap存储元素，它继承了HashSet，所有的方法和操作都与HashSet相同，因此LinkedHashSet的实现比较简单，只提供了 4个构造方法，并通过传递一个标识参数调用父类的构造器，在底层构造一个LinkedHashMap来记录数据访问，其他相关操作与父类HashSet相同，直接调用父类HashSet的方法即可。

#### MAP

**数组+链表存储数据，线程不安全**

##### HashMap

基于键的HashCode值唯一标识一条数据，同时基于键的HashCode值进行数据的存取，因此可以快速地更新和查询数据，但其每次遍历的顺序无法保证相同。HashMap的key和value允许为null。

HashMap是非线程安全的，即在同一时刻有多个线程同时写HashMap时将可能导致数据的不一致。如果需要满足线程安全的条件，则可以用Collections的synchronizedMap方法使HashMap具有线程安全的能力，或者使用ConcurrentHashMap。

为了减少链表遍历的开销，Java 8对HashMap进行了优化，将数据结构修改为数组+链表或红黑树。在链表中的元素超过 8个以后，HashMap会将链表结构转换为红黑树结构以提高查询效率，因此其时间复杂度为O(log N)。

##### ConcurrentHashMap

与HashMap不同，ConcurrentHashMap采用分段锁的思想实现并发操作，因此是线程安全的。ConcurrentHashMap由多个Segment组成（Segment的数量也是锁的并发度），每个Segment均继承自ReentrantLock并单独加锁，所以每次进行加锁操作时锁住的都是一个Segment，这样只要保证每个Segment都是线程安全的，也就实现了全局的线程安全。ConcurrentHashMap

在ConcurrentHashMap中有个concurrencyLevel参数表示并行级别，默认是 16，也就是说ConcurrentHashMap默认由 16个Segments组成，在这种情况下最多同时支持 16个线程并发执行写操作，只要它们的操作分布在不同的Segment上即可。并行级别concurrencyLevel可以在初始化时设置，一旦初始化就不可更改。ConcurrentHashMap的每个Segment内部的数据结构都和HashMap相同。

## 线程池、多线程

## 垃圾回收机制

## syncchronized

## volatile

# Hive

## 内部表外部表

### 区别

内部表的数据默认情况下会保存在hive.metastore.warehouse.dir的设置项的路径下，外部表可以自由指定路径

当我们删除一个内部表的时候，对应的数据也会被删除，外部表不会

内部表不方便和其他工作共享数据

## hive explain

## sql laterview explod

## 拉链表应用场景及实现

## 常见开窗函数

## Sql执行过程

## 常用sql

### uid，店铺每个店铺访问最多的top5

## 数据倾斜

### 原因

### 解决方案

# SPARK

## 常见的spark rdd

spark常见crach

# Hadoop

## namenode读写流程

### 使用客户端读取文件

访问namenode，告知要访问的文件

hdfs对client做身份信息验证，认证的方式有两种，一种是通过信任的客户端，由其指定用户名；第二种是通过诸如kerboers的强认证机制

检查文件的所有者以及其设定的访问权限，如果文件存在，且该用户对其有访问权限

此时namenode 会告诉hdfs客户端这个文件的第一个数据块的标识以及保存该数据块的datanode列表，此列表根据client和datanode之间的距离做了排序

有了数据块的标识和datanode列表主机名，hdfs便可以直接访问最合适的datanode读取所需要数据的数据块

这个过程直到该文件的所有数据块读取完成或HDFS客户端关闭文件流

### 使用客户端写文件

hdfs clint通过hdfs 相关api发送请求，打开要写入的文件。

如果该用户有写入文件的权限，那么该请求将被送达namenode，并建立该文件的元数据，但此时新建立的元数据并未和任何数据块相关联，此时hdfs客户端会收到打开文件成功的响应，此时就可以写入数据了

当客户端将数据写入流时，数据会被自动拆分成数据包，并将数据包保存在内存队列中

客户端会起一个独立的线程，他从队列中读取数据，并向namenode请求一组datanode列表，以便写入下一个数据块的多个副本

hdfs客户端将直接连接到列表中的第一个datanode，而该datanode又连接到第二个datanode，第二个又连接到第三个datanode，建立一个数据块的复制管道

复制管道中的每一个datanode都会确认所收到的数据包已经写入磁盘。hdfs客户端维护着一个列表，记录着哪些数据包尚未收到确认信息，每收到一个响应，客户端便知道数据已经成功写入管道中的datanode，客户端便知道数据已经成功写入到管道中的一个datanode

当数据块被写入列表中的datanode之后，HDFS客户端重新向namenode申请写下一组datanode，最终全部写入datanode，关闭数据管道并通知Namenode文件操作已经完成

### namenode

Filesystem image和FSimage以两种文件存在本地文件中，在每次namenode启动的时候都会加载最新的 File system image和Editlog

### MapReduce

#### map数量

mapreduce中map的数量控制有着一套算法，具体逻辑如下

```
defaultNum=totalSize/blockSize
expNum=mapred.map.tasks
expMaxNum=max(expNum,defaultNum)
splitMaxSize=totalSize/max(mapred.min.split.size,blockSize)
实际的map个数=min(realSplitNum, expMaxNum)
```

调整方法

##### 减少Map个数

需要增大mapred.min.split.size的值，减少mapred.map.tasks的值；

##### 增大Map个数

需要减少mapred.min.split.size的值，同时增大mapred.map.tasks的值。

#### 常用优化

##### 开起向量化查询

在默认情况下，在执行MapReduce过程中，mapper类里面有个run方法，在通过run（）调用setup（）方法，紧接着通过一个while循环调用map方法，**将一行行数据**循环发送给map（）方法进行处理，跳出循环后再调用cleanup（）方法，整个run（）方法结束.

在run（）方法中，我们看到map（）方法是逐行处理数据，这样的操作容易产生更多的CPU指令和CPU上下文切换，导致系统的处理性能不高。

hive对此提供了优化，可以调整为一次处理一条数据变为一次处理1万条数据，来提高程序的性能。开启向量模式的方法如下：

------

```
set hive.vectorized.execution.enabled = true;
```

**注意： 目前MapReduce计算引擎只支持Map端的向量化执行模式，Tez和Spark计算引擎可以支持Map和Reduce端的向量化执行模式。**

#### Shuffle

Shuffle过程按官方文档的解释是指代从Mapper的输出到Reduer输入的整个过程。但个人认为Shuffle的过程应该是从Mapper的Map方法输出到Reducer的Reduce方法输入的过程。它是制约MapReducer引擎性能的一个关键环节，但同时也保证了Hadoop即使能在一些廉价配置较低的服务器上可靠运行的一个环节。

在Mapper的Map方法中，context.write（）方法会将数据计算所在分区后写入到内存缓冲区，缓冲区的大小为mapreduce.task.io.sort.mb=100MB。当缓冲区缓存的数据达到一定的阀值mapreduce.map.sort.spill.percent=0.8，即总缓冲区的80%时，将会**启动新的线程将数据写入到HDFS临时目录**中。这样设计的目的在于避免单行数据频繁写，以减轻磁盘的负载。这与关系型数据库提倡批量提交（commit）有相同的作用。

在写入到HDFS的过程中，为了下游Reducer任务顺序快速拉取数据，会将数据进行排序后再写入临时文件中，当整个Map执行结束后会**将临时文件归并成一个文件**。如果不进行文件的排序归并，意味着下游Reducer任务拉取数据会频繁地搜索磁盘，即将顺序读变为随机读，这会对磁盘I/O产生极大的负载。

Reducer任务启动后，会启动拉取数据的线程，从HDFS拉取所需要的数据。为什么不选用Mapper任务结束后直接推送到Reducer节点，这样可以节省写入到磁盘的操作，效率更高？**因为采用缓存到HDFS，让Reducer主动来拉，当一个Reducer任务因为一些其他原因导致异常结束时，再启动一个新的Reducer依然能够读取到正确的数据**。

从HDFS拉取的数据，会先缓存到内存缓冲区，当数据达到一定的阈值后会将内存中的数据写入内存或者磁盘中的文件里。当从HDFS拉取的数据能被预先分配的内存所容纳，数据会将内存缓存溢出的数据写入该内存中，当拉取的数据足够大时则会将数据写入文件，文件数量达到一定量级进行归并。

#### 二次排序

# 数据仓库

## ODS层工作内容

## DWD层如何建模

## 维度表字段（时间维度字段）

## 数据仓库结构

## 如何看待数据治理

# 技术之外

## 自我介绍

## 对业务共享更大的一项工作

## 数据仓库和数据库的区别