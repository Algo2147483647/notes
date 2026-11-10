# Kafka

[TOC]


## Architecture

<img src="./assets/kafka_architecture.png" alt="kafka architecture" style="zoom:25%;" />

> [Apache Kafka Introduction Architecture | CloudDuggu](https://www.cloudduggu.com/kafka/architecture/)

- **Broker**
  - Kafka cluster has multiple nodes and each node represents a Kafka broker that contains multiple partitions that holds multiple topics.
- **Producer & Consumer**
  - Producers produce and send record to Kafka brokers for storage and distribution.
  - Consumer are appllications or services that subscribe to Kafka topics and read messages from them. They process the data perform various tasks based on the received messages.
- **Consumer Group**
  - In Kafka, a logical grouping of consumers is known as consumer groups.
- **Topic**
  - Topic defines the category in which the producer pumps the messages and depending upon the type of messages there is a new topic created.
  - producers publish messages to Topics.
  - Topics are similar to table in a database and represent a specific stream of records.

- **Partition**
  - ordered message queue
  - A partition contains ordered messages from the producer.
- **ZooKeeper** (in earlier versions)
  - used for cluster coordination and maintaining metadata.

## Process

消费者读取数据流程：

kafka linux sendfile技术 — 零拷贝

1. 消费者发送请求给kafka服务 

2. kafka服务去os cache缓存读取数据（缓存没有就去磁盘读取数据） 
3. 从磁盘读取了数据到os cache缓存中
4. os cache直接将数据发送给网卡
5. 通过网卡将数据传输给消费者

<img src="./assets/v2-5baa3063c6225ced2d03915a0ce5d666_720w.webp" alt="img" style="zoom: 50%;" />

## Other

顺序写磁盘、大量使用内存页 、零拷贝技术的使用

 顺序写入和 MMFile（Memory Mapped File）

所以硬盘最讨厌随机 I/O，最喜欢顺序 I/O

而且 Linux 对于磁盘的读写优化也比较多，包括 read-ahead 和 write-behind，磁盘缓存等

基于 Sendfile 实现零拷贝（Zero Copy）

