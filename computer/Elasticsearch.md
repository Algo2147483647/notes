# Elasticsearch

[TOC]

## Introduction

***What is Elasticsearch?***

> Elasticsearch is a distributed, RESTful search engine optimized for speed and relevance on production-scale workloads. Elasticsearch can be used to perform real-time search over massive datasets for applications including:
> - Vector search
> - Full-text search
> - Logs
> - Metrics
> - Application performance monitoring (APM)

***Why we need ES if we have MySQL?***

- Full-text search: MySQL, provides basic text search capabilities but may not offer the same level of performance and flexibility as Elasticsearch.

- Scalability and distributed architecture: MySQL is primarily designed for **vertical scaling**, and Elasticsearch is built to **scale horizontally**, where you add more resources to a single server. Elasticsearch's distributed architecture makes it well-suited for scenarios that require scalability and high availability. 

- Real-time data and analytics: Elasticsearch provides near real-time indexing and search capabilities. Elasticsearch's specialized features and speed make it more suitable for real-time data exploration and analysis.

- Unstructured and semi-structured data: Elasticsearch is schema-less and can handle unstructured and semi-structured data, such as JSON documents, log files, social media feeds, and sensor data. It allows you to index and search data without defining a fixed schema upfront. MySQL, on the other hand, is a relational database that requires predefined schemas and structured data.

- Text relevance and ranking: Elasticsearch's relevance and scoring mechanisms make it a preferred choice for applications where search result quality and relevance matter.

## Architecture of Elasticsearch 

<img src="../assets/word-image-141.png" alt="img" style="zoom: 67%;" />

- **Cluster & Node**: A cluster is a collection of one or more nodes (servers) that work together to store and process data. Each cluster is identified by a unique name. A node is an individual server that participates in a cluster. Each node holds a portion of the data, performs indexing and searching operations, and communicates with other nodes to maintain cluster health.
- **Index**: An index is a logical namespace that holds a collection of documents with similar characteristics. It is similar to a database in traditional databases. Each index has a unique name and is divided into shards.
- **Shards**: An index can be divided into multiple shards, allowing data to be distributed and processed in parallel across different nodes. Sharding improves scalability and performance. Shards can be primary or replica.
- **Document**: A document is the basic unit of information in Elasticsearch. It is a JSON object that can be indexed and searched. Documents are organized within an index and have a unique identifier (ID).
- **Replica**: Replicas are copies of shards. Elasticsearch automatically creates replica shards to provide fault tolerance and improve search performance. Replicas also enable parallel search operations.
- **Mapping**: Mappings defines how documents are stored and indexed. Mappings define the data types, field properties, and text analysis settings. By default, Elasticsearch automatically generates mappings based on the data.



Relation between RDBMS and Elasticsearch terms:

| Elasticsearch | RDBMS    |
| ------------- | -------- |
| Index         | Database |
| Type          | Table    |
| Document      | Row      |
| Field         | Column   |



## Indexing & Searching Data

### Inverted index

The inverted index is a database index storing a mapping from content to its locations in a table ($value \to key$). Where **Posting list** is an int array, which stores all document ids matching a certain term.

| Term (*Name*) | Posting List |
| :---: | :---: |
| Female | 2 |
| Male | [1,3] |

### Term Dictionary & Term Index

文本分析（Analysis）是把全文本转换一系列单词(term/token)的过程，也称为分词。

脑裂问题

## Elasticsearch Ecosystem: ELK

### Logstash

Logstash是一个开源数据收集引擎，具有实时管道功能。Logstash可以动态地将来自不同数据源的数据统一起来，并将数据标准化到你所选择的目的地。Logstash管道有两个必需的元素：输入和输出，以及一个可选元素：过滤器。输入插件从数据源那里消费数据，过滤器插件根据你的期望修改数据，输出插件将数据写入目的地。

### Kibana

K就是Kibana，Kibana是一个针对Elasticsearch的开源分析及可视化平台，用来搜索、查看交互存储在Elasticsearch索引中的数据。使用Kibana，可以通过各种图表进行高级数据分析及展示。ibana让海量数据更容易理解。它操作简单，基于浏览器的用户界面可以快速创建仪表板（dashboard）实时显示Elasticsearch查询动态。

<img src="assets/640-1689313318794-5.jpeg" alt="Image" style="zoom: 50%;" />

