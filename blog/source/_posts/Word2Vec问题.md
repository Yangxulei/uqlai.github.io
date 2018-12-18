---
title: Word2Vec理解
date: 2017-08-07 12:18:23
tags: Word2Vec
categories: NLP
---

带着问题看文章
- word2vec是怎么实现的？
看论文<!--more-->，先不总结

- Wordvec怎么得到词向量？
那么word2vec向量到底在哪儿？其实这些词向量就是神经网络里的参数，生成词向量的过程就是一个参数更新的过程。那么究竟是什么参数呢？就是这个网络的第一层：将one-hot向量转换成低维词向量的这一层（虽然大家都不称之为一层，但在我看来就是一层），因为word2vec的输入是one-hot。one-hot可看成是1*N（N是词总数）的矩阵，与这个系数矩阵（N*M, M是word2vec词向量维数）相乘之后就可以得到1*M的向量，这个向量就是这个词对应的词向量了。那么对于那个N*M的矩阵，每一行就对应了每个单词的词向量。接下来就是进入神经网络，然后通过训练不断更新这个矩阵。





参考：
[秒懂词向量Word2vec的本质](https://zhuanlan.zhihu.com/p/26306795)
[有谁可以解释下word embedding? - li Eta 的回答](https://www.zhihu.com/question/32275069/answer/61059440)
[有没有详细讲解word2vec的原理、具体应用、中文处理 方面的资料或教程？ - li Eta 的回答](https://www.zhihu.com/question/37677615/answer/73780047)
[Skip-gram如何训练得到词向量（ Distributed Representation）？ - li Eta 的回答](https://www.zhihu.com/question/29894719/answer/92783887)

