---
title: Preliminary Info of Spark
date: 2017-07-05 08:56:49
tags: Spark
categories: Spark
---
## What is Apache Spark?   
Apache Spark is a cluster computing platform designed to be fast and general-purpose.
<!-- more -->
On the speed side, Spark extends the popular MapReduce model to efficiently support more types of computations, including interactive queries and stream processing. One of the main features Spark offers for speed is the ability to run computations in memory, but the system is also more efficient than MapReduce for complex applications running on disk.

Apache Spark 是一款旨在快速通用的集群计算平台,在速度方面，扩展了流行的MapReduce模型，以有效支持更多类型的计算，包括交互式查询和流处理。能够在内存中运行计算，但是对于在磁盘上运行的复杂应用程序，该系统也比MapReduce更高效。


The Spark project contains multiple closely integrated components. At its core, Spark is a “computational engine” that is responsible for scheduling, distributing, and mon‐itoring applications consisting of many computational tasks across many worker machines, or a computing cluster. Because the core engine of Spark is both fast and general-purpose, it powers multiple higher-level components specialized for various workloads, such as SQL or machine learning. These components are designed to interoperate closely, letting you combine them like libraries in a software project。

Spark项目包含多个紧密集成的组件。其核心在于，Spark是一个“计算引擎”，负责在多个工作机器或计算集群中安排，分发和监视由许多计算任务组成的应用程序。由于Spark的核心引擎既快速又通用，因此可以为多种工作负载（如SQL或机器学习）提供专门的多个高级组件。这些组件的设计是为了与软件项目中的library进行紧密的交互操作。

We should learn the characteristics and benefits of its tight integration. Specific content, you can see "learning spark"。
我们应该学习它的紧密整合的特点和好处。具体的内容，可以看看《learning spark》

## Each of Spark’s components

![ Each of Spark’s components](
http://opdexhju0.bkt.clouddn.com/14992172107388.jpg)

#### Spark Core
Spark core includes the basic functions of Spark, including for task scheduling, memory management, fault recovery, and storage system interaction components. Spark Core also defines the Flexible Distributed Data Set (RDD) API. He provides a number of APIs for building and manipulating collections

Spark core 包含Spark的基本功能，包括用于任务调度，内存管理，故障恢复，与存储系统交互的组件。Spark Core 也是定义弹性分布式数据集(RDD)API所在。他提供了许多用于构建和操作集合的API

#### Spark SQL
Spark SQL is a spark package for handling structured data. It allows data to be queried through SQL. Is a variant of Apache Hive. Combine SQL with complex analysis.

Spark SQL是用于处理结构化数据的spark包。它允许通过SQL查询数据。是Apache Hive的变体。将SQL与复杂的分析相结合。

#### Spark Streaming
Spark Streaming is a Spark component that can handle real-time streaming data. At the same time, it provides an API for handling data streams that are closely related to the Spark Core RDD API. This is very convenient. And move between applications that store data on memory, on disk, or in real-time access. The same program has fault tolerance, throughput, and scalability as the Spark Core.

Spark Streaming 是一个Spark组件，可以处理实时流数据。同时，它提供了一个API用于处理与Spark Core RDD API密切相关的数据流。这是很方便的。而且操作存储在内存，磁盘上的或者实时访问中的数据的应用程序之间移动。与Spark Core有相同程序的容错能力，吞吐量和可扩展性。

#### MLIb 
This is a library of common machine learning functions that provide many types of machine learning algorithms, including classification, regression, clustering, and collaborative filtering. It also provides some lower level ML primitives, including gradient descent optimization algorithms. So these methods can be designed to expand the cluster expansion, is not it amazing?

这是一个通用机器学习功能的库，提供很多类型的机器学习算法，包括分类，回归，聚类和协同过滤等等。它还提供了一些较低级别的ML原语，包括梯度下降优化算法。所以的这些方法都可以被设计为扩集群扩展，是不是很amazing呢？

#### GraphX
GraphX is a library for manipulating graphics and performing graphical parallel computing. It also extends the Spark RDD API, allowing the user to create a directed graph with arbi-trary attributes attached to each vertex and edge. GraphX also provides a variety of operators for manipulating graphics and a library of common graphics algorithms.

Graphx 是用于操作图形和执行图形并行计算的库，它也扩展了Spark RDD API，允许使用者创建一个连接到每个顶点和边缘的具有arbi-trary属性的有向图。GraphX还提供了各种用于操作图形的操作器和一个常见图形算法库。

#### Cluster Managers(集群管理器)
Under the engine, Spark is designed to effectively extend from one to thousands of compute nodes. How to achieve and maximize flexibility? So with the cluster manager. Spark can run on a clustered manager, including Hadoop YARN, Apache Mesos, and a simple cluster manager that is included in Spark itself as a separate scheduler. This concept is far from the current far, and so learn to write later, first we just  know  this concept.

在引擎下，Spark旨在有效地从一个到数千个计算节点扩展。怎么实现而且最大限度地提升灵活性？于是有了集群管理器。Spark可以运行在在中集群管理器上，包括Hadoop YARN，Apache Mesos，以及包含在Spark本身称为独立调度程序的简单集群管理器。这个概念离目前有点远，等学到后面再写，先知道有这个概念就好。




具体的可以看看Spark的官方文档。



