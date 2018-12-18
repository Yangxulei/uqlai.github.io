---
title: 初识CAP Theorem
date: 2017-07-27 23:01:51
tags: CAP
categories: 杂知识
---
在”地铁图“的1-Funcdamentals部分看到了这个[CAP Theorem(CAP定理)](https://zh.wikipedia.org/wiki/CAP定理)，<!--more-->不知道是啥，好奇下wiki了下，大概知道了点

它又被称作**布鲁尔定理**（Brewer's theorem），它指出对于一个[分布式计算系统](https://zh.wikipedia.org/wiki/%E5%88%86%E5%B8%83%E5%BC%8F%E8%AE%A1%E7%AE%97)来说，不能同时满足C(Consistence),A([Availability](https://zh.wikipedia.org/wiki/%E5%8F%AF%E7%94%A8%E6%80%A7)),P([Network partitioning](https://zh.wikipedia.org/w/index.php?title=Partition_tolerance&action=edit&redlink=1))  看到这我也不懂啊，肿么办，知识还是太少，还是不知道干啥的，耐心看了。

CAP 定理是分布式系统理论的基础，它的核心内容是说，在存在分区（如网络故障）的情况下，一个系统无法同时保证一致性（consistency）和可用性（availability），只能二选其一。理解CAP理论的最简单方式是想象两个节点分处分区两侧。允许至少一个节点更新状态会导致数据不一致，即丧失了C性质。如果为了保证数据一致性，将分区一侧的节点设置为不可用，那么又丧失了A性质。除非两个节点可以互相通信，才能既保证C又保证A，这又会导致丧失P性质。

感觉到这就好了，可能高可用，分布式等会更多接触和理解吧，毕竟只是理论，先知道这个就好，下面给些资料。

-  Nancy Lynch and Seth Gilbert, [“Brewer's conjecture and the feasibility of consistent, available, partition-tolerant web services”](http://lpd.epfl.ch/sgilbert/pubs/BrewersConjecture-SigAct.pdf), *ACM SIGACT News*, Volume 33 Issue 2 (2002), pg. 51-59.
-  [CAP理论十二年回顾："规则"变了](http://www.infoq.com/cn/articles/cap-twelve-years-later-how-the-rules-have-changed).
-  ["Brewer's CAP Theorem"](http://www.julianbrowne.com/article/viewer/brewers-cap-theorem), julianbrowne.com, Retrieved 02-Mar-2010

