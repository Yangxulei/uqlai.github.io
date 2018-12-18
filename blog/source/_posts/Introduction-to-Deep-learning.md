---
title: '初识吴恩达深度学习课程'
date: 2017-08-10 09:40:03
tags:
categories: DeepLearning
---
![WX20170809-201529.png](http://upload-images.jianshu.io/upload_images/744392-1bcb67da64482f1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这是Ng吴恩达老师的全新Ai项目 www.deeplearning.ai，早些已经学完他的ML课程，从此走了ML道路，现在开深度学习课程很开心
<!--more-->

写这篇主要是介绍深度学习
- What is a neural network?
-  Supervised Learning with NN
- Why is Deep Learning taking off?

# What is a neural network?
和ML课程一样，首先引出了房价预测的案例来展开

![线性回归示意](http://upload-images.jianshu.io/upload_images/744392-03743b0c6d467fb7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
解释下这个蓝色线段，因为房价不会是负的，所以没有拟合的慢慢会为0，这个其实就是Relu功能。其实也可以看做是最简单的神经网络，单细胞生物似的。影响房价的因素有很多，上面单一的组合起来就形成了网络，看下图。
![多因素神经网络示意图](http://upload-images.jianshu.io/upload_images/744392-5caa0151ef4fbe5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![形式化表达一下](http://upload-images.jianshu.io/upload_images/744392-80c88bd11d81efb1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

具体可以看这篇文章[[重磅！神经网络浅讲：从神经元到深度学习](http://www.36dsj.com/archives/39775)](http://www.36dsj.com/archives/39775)这些概念和历史也不作重点在这里介绍。

# Supervised Learning with NN

机器学习又分为监督学习和无监督学习，这些概念需要我们知道，在监督学习中，通过输入一些x，得到想要学习映射到某个输出y的函数。例如，刚刚我们看到房价预测应用程序，您输入一些家庭的某些特征，并尝试输出或估计价格y。这里有一些其他的例子，神经网络已被非常有效地应用

![神经网络案例](http://upload-images.jianshu.io/upload_images/744392-bd166bf6a21279f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


房地产和在线广告可能是一个相对标准的神经网络，对于图像应用，经常使用卷积神经网络，通常缩写为CNN，并用于序列数据。音频是一个时间分量？随着时间的推移播放音频，所以音频最自然地表示为一维时间序列或一维时间序列。因此，对于序列数据，经常使用RNN。语言，英文和中文，字母或单词一次一个，所以语言也最自然地表现为序列数据。因此，这些应用程序经常使用更复杂的RNN版本。对于更复杂的应用程序，如自主驾驶中，图片和雷达信息是一个完全不同的。可能会使用一个更为自定义或者更复杂的混合神经网络架构。

![部分神经网络](http://upload-images.jianshu.io/upload_images/744392-98e39ee19dc9ca1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在数据类型中通常会遇到结构化和非结构化的数据，数据类型这这里先不展开，后面的技术都是围绕着这两种类型展开的。
![数据类型](http://upload-images.jianshu.io/upload_images/744392-edf5467df7f7d27a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## Why is  DL taking off?
总结下来就6方面，更多的需要自己去了解回归深度学习的发展了。
- 数据
- 算法
- 计算力
- idea
- code
- experience
（完）

