---
title: 'Logistic Regression as a NN'
date: 2017-08-17 08:43:26
categories: DeepLearning
tags: Logistic
---

正式开始前先说一些关于统计学习的东西有个整体的大局观

统计的三要素：模型，策略，和算法
<!--more-->
模型：是要学习的条件概率分布或者决策函数。
策略：就是要按照怎么的学习规则学习或者选择最优模型，损失函数度量一次预测的好坏，风险函数度量平均意义下模型预测的好坏
算法：学习模型的具体计算方法，在统计中归结为最优化算法

在监督学习中会从假设空间中选取模型 f作为决策函数，给定输入X由f(X)给出相应的输出Y， 用损失函数或者代价函数来度量预测的好坏程度。模型选择的典型方法是正则化，是结构风险最小化策略的实现。其它还有交叉验证。

常见损失函数有：
-  0-1 loss function
-  quadratic loss function
- absolute loss function
- logarithmic loss function/loglikelihood loss function : L(Y,P(Y|X)) = -logP(Y|X)

我们知道监督学习的任务是学习模型：决策函数Y=f(X)或者条件概率分布P(Y|X),监督学习的方法可分为 生成方法 和 判别方法 。它们对应学到的模型就是生成模型(朴素贝叶斯法和隐马尔科夫模型)和 判别模型（K近邻法，感知机，决策树，逻辑斯蒂回归模型，最大熵模型，支持向量机，提升方法和条件随机场）

用监督学习的核心问题大概有分类，标注，回归。

这节所说逻辑斯蒂回归其实就是个二分类算法。比如0或者1。先看下Binary Classification。

![识别猫](http://upload-images.jianshu.io/upload_images/744392-9ec7e25f3009755d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果输入一张64X64的图片，来识别是否为猫，用Y来表示输入，在过程中，会把图片转成64乘64的三个矩阵，因为图片三原色红蓝绿呗，看上图，将像素强度值展开转到特征向量Y中，直到我们得到一个非常长的特征向量列出了该图像的所有红色和蓝色，绿色像素强度值，所以一个64×64图像的总尺寸这个向量X将是64×64乘3，这个矩阵的结果是1 2 2 8 8，使用小写n来表示该输入特征向量的维度，因此在二进制分类中，我们的目标是学习可以输入由该特征向量X表示的图像的分类器，并且预测相应的标号Y是否为1或0，其中X是nx维特征向量，Y标签是0或1

![一些数学表示](http://upload-images.jianshu.io/upload_images/744392-07ce408704385a66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

课程中的问题：Can the training set and test set have overlapping (x,y)pairs? No

#Logistic Regression
![logistic regression 数学表达](http://upload-images.jianshu.io/upload_images/744392-99ec8fca7a399035.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
看上图表达已经很清楚了，有时候数据很大或者很小，我们没法比较，所以能不能把数据经过处理后就可以比较了呢，所以通过logistics表达式后值域为(0,1)。


#Logistic Regression Cost

![logistics cost function](http://upload-images.jianshu.io/upload_images/744392-2425c6a2d7c20d07.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# LR的优缺点：
- LR分类器适用数据类型：数值型和标称型数据。
- 其优点是计算代价不高，易于理解和实现；
- 其缺点是容易欠拟合，分类精度可能不高。

重点要掌握的：
LR的优缺点和推导
写LR目标函数，目标函数怎么求最优解

[之前的文章和总结](http://www.jianshu.com/p/4db93e9f38af)
[更详细的文章](https://zhuanlan.zhihu.com/p/28057866)
参考：
李航《统计学习方法》

