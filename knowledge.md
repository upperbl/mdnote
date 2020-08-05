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

### namenode

Filesystem image和FSimage以两种文件存在本地文件中，在每次namenode启动的时候都会加载最新的 File

### MapReduce之后形成几个文件

## MapReduce二次排序

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