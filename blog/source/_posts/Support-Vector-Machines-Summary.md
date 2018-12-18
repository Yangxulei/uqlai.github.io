---
title: Support Vector Machines Summary
date: 2017-05-20 18:36:20
tags: SVM
categories: MachineLearning
---
经过最近的学习了解了部分理论但是没有实践应用，所以先写下来，可能不准确。
### 定义：
在reddit上看到一个很好的解释更直观和生动：
[如何向一个五岁的孩子解释SVM](https://www.reddit.com/r/MachineLearning/comments/15zrpp/please_explain_support_vector_machines_svm_like_i/)
知乎上也有人提到这个，而且已经整理如下：[中文](https://www.zhihu.com/question/21094489)
<!-- more -->

[wiki定义](https://en.wikipedia.org/wiki/Support_vector_machine):其实就是个监督学习模型，用来分析回归和分类，它巧妙的运用非线性变换把低维的特征投影到高维，可以执行比较复杂的分类任务（升维打击），是一种二类分类模型。它的基本模型是定义在特征空间上的间隔最大的线性分类器，间隔最大使它有别于感知机；

包含了构建从简单到复杂的模型：线性可分支持向量机（linear support vector machine in linearly separable case)、线性支持向量机（linear support vector machine)及非线性支持向量机（non-linear support vector machine)。简单模型是复杂模型的基础，也是复杂模型的特殊情况。（具体可以看李航老师的《统计学习方法》）

### 1基本问题
在[知错能改的感知机](http://uqlai.cn/2017/05/10/%E7%9F%A5%E9%94%99%E8%83%BD%E6%94%B9%E7%9A%84%E6%84%9F%E7%9F%A5%E6%9C%BA/)中，学习到在线性可分的训练数据中，我们可以得到不能分分类界线
![](
http://opdexhju0.bkt.clouddn.com/14952791835673.jpg)

为了得到最大边界间隔的超平面，将问题准换为优化问题，期中margin(b,w)表示超平面wx+b 离样本的最小距离，进而让这个最小距离最大化：
![](
http://opdexhju0.bkt.clouddn.com/14952778382070.jpg)
描述距离：
![描述距离](
http://opdexhju0.bkt.clouddn.com/14952779512133.jpg)
距离推导的结果：
![](
http://opdexhju0.bkt.clouddn.com/14952780106684.jpg)
将问题转化为：
![](
http://opdexhju0.bkt.clouddn.com/14952781553706.jpg)
进一步简化，因为w和b同时成倍的放缩不会影响超平面的变化，所以总可以找到一组w* *和b**使得miny(**wx+b* *)=1,所以有
![](
http://opdexhju0.bkt.clouddn.com/14952785985439.jpg)
当然可以用反正法证明一下，假设

y(**wx+b* *)>1， 我们可以通过放缩w，b得到更优化的解，约束条件和下图等价
![](
http://opdexhju0.bkt.clouddn.com/14952787703405.jpg)
最后得到上图的优化问题，这个问题的形式和二次规划（线性规划的进阶版）一致，所以可以用二次规划的方法解决。
### 2可行性
因为svm对噪声的容忍性更强，所以从VC bound 角度讲(超平面到底能产生多少圈圈叉叉分类的组合)，对于PLA来说可以shatter所有组合，但svm会对margin有限制
![](
http://opdexhju0.bkt.clouddn.com/14952797116001.jpg)
linear hard SVM不能shatter任意三个inputs，说明有更少的维度，所以有更好的泛化能力。同时，使用特征转化，可以使Linear hard SVM 进行更精细分类。

![](
http://opdexhju0.bkt.clouddn.com/14952798405661.jpg)
### 使用场景
SVM的典型使用场景如： 
一、房价估算
根据过去十年来房价和房屋面积、卧室数量、当地消费水平等等各种因素数据，将房屋分为「豪宅」、「中等」、「经济型住房」、「贫民窟」等几类；
使用SVM训练这些数据得出一个模型，可以用来预测在新的条件下，某个住房可以被划归到哪种分类，价值区间多少。

二、垃圾邮件分类器：
获取可疑的spam email关键词列表，例如：Buy、now等（实际Spam Corpus可以参考使用Apache Spam Assassin）；
收集大量的spam和非spam邮件数据，将其中包含的可疑spam关键词找出并标记在特征向量中，用SVM训练这些数据，得出一个模型，用来判断一封新的邮件是否为一个垃圾邮件。


####其实SVM最难的在于各种核函数，包括选取，这个在后面的文章中再说。
### Reference：
台大林老师《机器学习技法》
李航《统计学习方法》



###扩展阅读：
- http://www.hankcs.com/ml/support-vector-machine.html
- 《机器学习实战》
- https://www.zhihu.com/search?type=content&sort=upvote&q=%E6%94%AF%E6%8C%81%E5%90%91%E9%87%8F%E6%9C%BA


