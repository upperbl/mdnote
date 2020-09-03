master
# JAVA
~
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

### String+Stringbuilder+StringBuffer

## 线程池、多线程

## 垃圾回收机制

## syncchronized

## volatile

# Hbase

### hbase热点问题

#### 原因

#### 解决方案

# Kafka

### kafka消费顺序问题

### 如何保证数据按顺序消费

# Sqoop

## 多线程拉取数据

如果线程挂了如何保证数据一致性问题

# Hive

## 架构分析

## Driver

## metastore元数据管理

## hive thiftserver

## 内部表外部表

### 区别

内部表的数据默认情况下会保存在hive.metastore.warehouse.dir的设置项的路径下，外部表可以自由指定路径

当我们删除一个内部表的时候，对应的数据也会被删除，外部表不会

内部表不方便和其他工作共享数据

## hive explain

查看执行计划的基本信息，即explain；

查看执行计划的扩展信息，即explain extended；

查看SQL数据输入依赖的信息，即explain dependency；

查看SQL操作相关权限的信息，即explain authorization；

查看SQL的向量化描述信息，即explain vectorization。

## SQL优化

### 优化join sql

```
--代码片段1
select a.s_no 
from student_orc_partition  a
inner join student_orc_partition_only b
on a.s_no=b.s_no and a.part=b.part and a.part>=1 and a.part<=2
--代码片段2
select a.s_no 
from student_orc_partition  a
inner join student_orc_partition_only b
on a.s_no=b.s_no and a.part=b.part
where a.part>=1 and a.part<=2
```

上面两个代码块看似一样，但是执行起来会有很大的区别，我们使用 explain dependency 查看执行依赖

```
--代码片段1的explain dependency打印结果：
{"input_partitions":
[{"partitionName":"default@student_orc_partition@part=0"},
{"partitionName":"default@student_orc_partition@part=1"},
{"partitionName":"default@student_orc_partition@part=2"},
{"partitionName":"default@student_orc_partition_only@part=1"},
{"partitionName":"default@student_orc_partition_only@part=2"}],
"input_tables":
[{"tablename":"default@student_orc_partition","tabletype":"MANAGED_TABLE"},
{"tablename":"default@student_orc_partition_only","tabletype":"MANAGED_TABLE"}]}
--代码片段2的explain dependency打印结果：
{"input_partitions":
[{"partitionName":"default@student_orc_partition@part=1"},
{"partitionName" : "default@student_orc_partition@part=2"},
{"partitionName" :"default@student_orc_partition_only@part=1"},
{"partitionName":"default@student_orc_partition_only@part=2"}],
"input_tables":
[{"tablename":"default@student_orc_partition","tabletype":"MANAGED_TABLE"},
{"tablename":"default@student_orc_partition_only","tabletype":"MANAGED_TABLE"}]}

```

通过上面的输出结果可以看到，其实上述的两个SQL并不等价，在内连接（inner join）中的连接条件中加入非等值的过滤条件后，并没有将内连接的左右两个表按照过滤条件进行过滤，内连接在执行时会多读取part=0的分区数据。

可以看到，对左外连接在连接条件中加入非等值过滤的条件，如果过滤条件是作用于右表（b表）有起到过滤的效果，则右表只要扫描两个分区即可，但是左表（a表）会进行全表扫描。如果过滤条件是针对左表，则完全没有起到过滤的作用，那么两个表将进行全表扫描。这时的情况就如同全外连接一样都需要对两个数据进行全表扫描。

 如果要使用外连接并需要对左、右两个表进行条件过滤，最好的方式就是将过滤条件放到表的就近处，即如果已经知道表数据过滤筛选条件，那么在使用该表前，就用该过滤条件进行过滤，一些SQL内置优化器也会做上述的优化，例如下sql

```
select a.s_no 
from （
  select s_no,part
  from student_orc_partition
  --在子查询内部进行过滤
  where part>=1 and part<=2
）  a
left outer join student_orc_partition_only b
on a.s_no=b.s_no and a.part=b.part ;
```

## 常见hive SQL考察

说明，关于内置的hive的udf函数使用，建议直接参考hive 官方wiki https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-explode(array)

### UDF考察

#### explode

`explode()` takes in an array (or a map) as an input and outputs the elements of the array (map) as separate rows. UDTFs can be used in the SELECT expression list and as a part of LATERAL VIEW.

As an example of using `explode()` in the SELECT expression list, consider a table named myTable that has a single column (myCol) and two rows:

| Array<int> myCol |
| :--------------- |
| [100,200,300]    |
| [400,500,600]    |

Then running the query:

```
SELECT explode(myCol) AS myNewCol FROM myTable;
```

will produce:

| (int) myNewCol |
| :------------- |
| 100            |
| 200            |
| 300            |
| 400            |
| 500            |
| 600            |

The usage with Maps is similar:

```
SELECT` `explode(myMap) ``AS` `(myMapKey, myMapValue) ``FROM` `myMapTable;
```

#### lateral view explod

```
SELECT * FROM `default`.`testlater`;
```

| pageid      | addlist |
| ----------- | ------- |
| frontpage   | [1,2,3] |
| contactpage | [4,5,6] |

```
select pageid , t1 from  testlater  lateral view explode(split(regexp_replace(addlist,"\\[|\\]",""),","))a as t1
```

| **pageid**  | **t1** |
| ----------- | ------ |
| frontpage   | 1      |
| frontpage   | 2      |
| frontpage   | 3      |
| contactpage | 4      |
| contactpage | 5      |
| contactpage | 6      |

lateral view用于和split, explode等UDTF一起使用，它能够将一行数据拆成多行数据，在此基础上可以对拆分后的数据进行聚合。lateral view首先为原始表的每行调用UDTF，UDTF会把一行拆分成一或者多行，lateral view再把结果组合，产生一个支持别名表的虚拟表。

由此可见，lateral view与explode等udtf就是天生好搭档，explode将复杂结构一行拆成多行，然后再用lateral view做各种聚合。

### 开窗函数考察

**目录**

[浅谈hive常用窗口函数](https://blog.csdn.net/liu82327114/article/details/106017532#浅谈hive常用窗口函数)

[简介](https://blog.csdn.net/liu82327114/article/details/106017532#简介)

[常用窗口函数](https://blog.csdn.net/liu82327114/article/details/106017532#常用窗口函数)

[over](https://blog.csdn.net/liu82327114/article/details/106017532#over（）)

[SUM,AVG,MIN,MAX](https://blog.csdn.net/liu82327114/article/details/106017532#SUM%2CAVG%2CMIN%2CMAX)

[NTILE](https://blog.csdn.net/liu82327114/article/details/106017532#NTILE)

[ROW_NUMBER](https://blog.csdn.net/liu82327114/article/details/106017532#ROW_NUMBER)

[RANK & DENSE_RANK](https://blog.csdn.net/liu82327114/article/details/106017532#RANK %26 DENSE_RANK)

[CUME_DIST&PERCENT_RANK](https://blog.csdn.net/liu82327114/article/details/106017532#CUME_DIST%26PERCENT_RANK)

[LAG](https://blog.csdn.net/liu82327114/article/details/106017532#LAG)

[LEAD](https://blog.csdn.net/liu82327114/article/details/106017532#LEAD)

[FIRST_VALUE&LAST_VALUE](https://blog.csdn.net/liu82327114/article/details/106017532#FIRST_VALUE%26LAST_VALUE)

## 

窗口函数又名开窗函数，属于分析函数的一种，用于解决复杂报表统计需求的功能强大的函数。窗口函数用来计算基于组的某种聚合值，它和聚合函数的不同之处是：对于每个组返回多行，而聚合函数对于每个组只返回一行。

开窗函数指定了分析函数工作的数据窗口大小，这个数据窗口大小可能会随着行的变化而变化。

#### over

- over() 通常与聚合函数共同使用，比如 count()、sum()、min()、max()、avg() 等。
- over() 具有一定的窗口语义 ，如：OVER(ROWS ((CURRENT ROW) | (UNBOUNDED) PRECEDING) AND (UNBOUNDED |(CURRENT ROW) ) FOLLOWING )，不过这些窗口定义经常与聚合函数（sum min max）相结合使用，像一些序列函数（row number、rank等）是不可以使用的
- over() 直接使用时，通常是指定全量数据，当我们想要按某列的不同值进行窗口划分时，可以在 over() 中加入 partition by 语句。

**在单独进行明细和count聚合的时候都会报错，但是加上窗口就可以正常执行**

```
select *,count(*)  from t_dw_orders_his
-------------------------------------------------------------------------------------------
Error while compiling statement: FAILED: SemanticException [Error 10025]: Expression not in GROUP BY key orderid
select *,count(*) over() from t_dw_orders_his  where p_event_date="2015-08-22"
//可以正常得到结果
10	2015-08-22	2015-08-22	支付	2015-08-22	9999-12-31	2015-08-22	17
9	2015-08-22	2015-08-22	创建	2015-08-22	9999-12-31	2015-08-22	17
8	2015-08-21	2015-08-22	支付	2015-08-22	9999-12-31	2015-08-22	17
8	2015-08-21	2015-08-21	创建	2015-08-21	2015-08-21	2015-08-22	17
7	2015-08-20	2015-08-21	支付	2015-08-21	9999-12-31	2015-08-22	17
7	2015-08-20	2015-08-21	支付	2015-08-20	2015-08-20	2015-08-22	17
6	2015-08-20	2015-08-22	支付	2015-08-22	9999-12-31	2015-08-22	17
6	2015-08-20	2015-08-20	创建	2015-08-20	2015-08-21	2015-08-22	17
5	2015-08-19	2015-08-20	支付	2015-08-19	9999-12-31	2015-08-22	17
4	2015-08-19	2015-08-21	完成	2015-08-21	9999-12-31	2015-08-22	17
4	2015-08-19	2015-08-21	完成	2015-08-19	2015-08-20	2015-08-22	17
3	2015-08-19	2015-08-21	支付	2015-08-21	9999-12-31	2015-08-22	17
3	2015-08-19	2015-08-21	支付	2015-08-19	2015-08-20	2015-08-22	17
2	2015-08-18	2015-08-22	完成	2015-08-22	9999-12-31	2015-08-22	17
2	2015-08-18	2015-08-18	创建	2015-08-18	2015-08-21	2015-08-22	17
1	2015-08-18	2015-08-22	支付	2015-08-22	9999-12-31	2015-08-22	17
```

#### SUM,AVG,MIN,MAX

此类聚合函数用户类似，在此我们以SUM为例结合OVER的窗口语句进行总结

准备数据

```
CREATE TABLE orders1(
  `orderid` int, 
  `createtime` string, 
  `money` int)
-----------------------
SELECT * FROM orders1
-----------------------
1	2015-08-18	72
1	2015-08-19	19
1	2015-08-20	67
1	2015-08-21	78
1	2015-08-22	62
1	2015-08-23	62
```

各种over参数情况下效果如下

```sql
SELECT orderid,
createtime,
money,
SUM(money) OVER() AS money1,
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC) AS money2, 
SUM(money) OVER(PARTITION BY orderid ORDER BY  createtime ASC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS money3, 
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN 3 PRECEDING AND CURRENT ROW) AS money4,
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN 3 PRECEDING AND 1 FOLLOWING) AS money5,   
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS money6   
FROM orders1;
```

结果如图

![img](https://img-blog.csdnimg.cn/20200509153639506.png)

总结

PRECEDING：往前数几行
FOLLOWING：往后
CURRENT ROW：当前行
UNBOUNDED：起点，UNBOUNDED PRECEDING 表示从前面的起点， UNBOUNDED FOLLOWING：表示到后面的终点

特别注意当上面的那个demo如果createtime有重复值,则会意想不到的效果，结果如下面请参考

```sql
SELECT * FROM orders1
1	2015-08-18	72
1	2015-08-18	72
1	2015-08-19	78
1	2015-08-19	19
1	2015-08-19	72
1	2015-08-20	62
1	2015-08-20	62
1	2015-08-21	67
1	2015-08-22	78
1	2015-08-22	24
1	2015-08-23	67
1	2015-08-23	19
1	2015-08-23	19
同样的执行下面这个sql
SELECT orderid,
createtime,
money,
SUM(money) OVER() AS money1,
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC) AS money2, 
SUM(money) OVER(PARTITION BY orderid ORDER BY  createtime ASC ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS money3, 
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN 3 PRECEDING AND CURRENT ROW) AS money4,
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN 3 PRECEDING AND 1 FOLLOWING) AS money5,   
SUM(money) OVER(PARTITION BY orderid ORDER BY createtime ASC ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS money6   
FROM orders1;
```

结果如下

![img](https://img-blog.csdnimg.cn/20200509154010490.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdTgyMzI3MTE0,size_16,color_FFFFFF,t_70)

#### NTILE

NTILE(n)，切片函数，用于将分组数据按照顺序切分成n片，返回当前切片值，如果切片不均匀，默认增加第一个切片的分布

准备数据如下

```
CREATE TABLE orders1(
  `orderid` int, 
  `createtime` string, 
  `money` int)
-----------------------
SELECT * FROM orders1
-----------------------
1	2015-08-18	72
1	2015-08-19	19
1	2015-08-20	67
1	2015-08-21	78
1	2015-08-22	62
1	2015-08-23	62
```

执行sql效果如下

```sql
SELECT 
orderid,
createtime,
money,
NTILE(2) OVER(PARTITION BY orderid ORDER BY createtime) AS rn1,
NTILE(3) OVER(PARTITION BY orderid ORDER BY createtime) AS rn2,
NTILE(4) OVER(ORDER BY createtime) AS rn3
FROM orders1 
```

结果如下，可以注意下分成4个切片的情况，数据共有6组，分成4组切片的时候每组不足两个，结果第三组和第四组各有1个

![img](https://img-blog.csdnimg.cn/20200509155332729.png)

#### ROW_NUMBER

ROW_NUMBER() –从1开始，按照顺序，生成分组内记录的序列，这个函数是非常常用的一个窗口函数，应用场景非常广泛，如在各种求日活月活的场景（配合where rn=1的用法比较多）

```
SELECT 
orderid,
createtime,
money,
row_number() OVER(PARTITION BY orderid ORDER BY createtime) AS rn
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509160114961.png)

#### RANK & DENSE_RANK

—RANK() 生成数据项在分组中的排名，排名相等会在名次中留下空位,数字是不连续的
—DENSE_RANK() 生成数据项在分组中的排名，排名相等会在名次中不会留下空位，数字是连续的

```
SELECT 
orderid,
createtime,
money,
rank() OVER(PARTITION BY orderid ORDER BY money) AS rn1,
dense_rank() OVER(PARTITION BY orderid ORDER BY money) AS rn2
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509161143320.png)

#### CUME_DIST&PERCENT_RANK

–CUME_DIST 小于等于当前值的行数/分组内总行数
–比如，统计小于等于当前薪水的人数，所占总人数的比例

–PERCENT_RANK 分组内当前行的RANK()函数值-1/分组内总行数-1

```
SELECT 
orderid,
createtime,
money,
cume_dist() OVER(PARTITION BY orderid ORDER BY money) AS rn1,
percent_rank() OVER(PARTITION BY orderid ORDER BY money) AS rn2,
rank() OVER(PARTITION BY orderid ORDER BY money) AS rn3
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509163101356.png)

#### LAG

LAG(col,n,DEFAULT) 用于统计窗口内往上第n行值
第一个参数为列名，第二个参数为往上第n行（可选，默认为1），第三个参数为默认值（当往上第n行为NULL时候，取默认值，如不指定，则为NULL）

```
SELECT 
orderid,
createtime,
money,
lag(money,1,null) OVER(PARTITION BY orderid ORDER BY money) AS rn1,
lag(money,2,22) OVER(PARTITION BY orderid ORDER BY money) AS rn2,
lag(money,3,33) OVER(PARTITION BY orderid ORDER BY money) AS rn3
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509165300194.png)

#### LEAD

与LAG相反
LEAD(col,n,DEFAULT) 用于统计窗口内往下第n行值
第一个参数为列名，第二个参数为往下第n行（可选，默认为1），第三个参数为默认值（当往下第n行为NULL时候，取默认值，如不指定，则为NULL）

```
SELECT 
orderid,
createtime,
money,
lead(money,1,null) OVER(PARTITION BY orderid ORDER BY money) AS rn1,
lead(money,2,22) OVER(PARTITION BY orderid ORDER BY money) AS rn2,
lead(money,3,33) OVER(PARTITION BY orderid ORDER BY money) AS rn3
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509165520767.png)

#### FIRST_VALUE&LAST_VALUE

--FIRST_VALUE取分组内排序后，截止到当前行，第一个值

--LAST_VALUE取分组内排序后，截止到当前行，最后一个值

```
SELECT
orderid,
createtime,
money,
first_value(money) OVER(PARTITION BY orderid ORDER BY money) AS rn1,
last_value(money) OVER(PARTITION BY orderid ORDER BY money) AS rn2,
first_value(money) OVER(PARTITION BY orderid ORDER BY money desc) AS rn11,
last_value(money) OVER(PARTITION BY orderid ORDER BY money desc) AS rn22
FROM orders1 
```

![img](https://img-blog.csdnimg.cn/20200509170119285.png)

#### 

### uid，店铺每个店铺访问最多的top5

### 连续访问topN

uid,dianpu,date 找出一个月内访问连续访问这个店铺超过五天的uid

### 拉链表应用场景及实现

### 去重方法和应用逻辑

## Sql执行过程

## 数据倾斜

### 原因

### 解决方案

# SPARK

## hive和spark比较

### 哪个用的多

### 哪个稳定性高一点

### spark core里面的stage job task角色关系

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

#### 常用mr优化

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

## 数据血缘问题

## 数据仓库和数据库的区别

## 概念

## 中台区别

## ODS层工作内容

## DWD层如何建模

## 维度表字段（时间维度字段）

## 数据仓库结构

## 如何看待数据治理

# 技术之外

## 自我介绍

## 对业务共享更大的一项工作

## 核心竞争力

## 项目中的骄傲点
