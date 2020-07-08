# Flink笔记

## 状态管理器

### 状态类型

#### Keyed State

##### 特点

跟于KeyedStream类型后面，一定用在KeyedStream后面，使用时要判断上一个算子的数据类型的返回值

keyed state事先按照key对数据进行了分区，每个key state 对应一个operator 和key的组合

#### Operated State

### 存在形式

#### 托管状态（Managed State）

由Flink Runtime中控制和管理状态数据，并将状态数据转换成为内存Hash tables或RocksDB的对象存储，然后将这些状态数据通过内部的接口持久化到Checkpoints中，任务异常时可以通过这些状态数据恢复任务

#### 原生状态（Row State）

，由算子自己管理数据结构，当触发Checkpoint过程中，Flink并不知道状态数据内部的数据结构，只是将数据转换成bytes数据存储在Checkpoints中，当从Checkpoints恢复任务时，算子自己再反序列化出状态的数据结构

#### 两种形态比较

DataStream API支持使用Managed State和Raw State两种状态形式，在Flink中推荐用户使用Managed State管理状态数据，主要原因是Managed State能够更好地支持状态数据的重平衡以及更加完善的内存管理