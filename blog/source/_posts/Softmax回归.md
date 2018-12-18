---
title: Softmax回归
date: 2017-08-03 18:34:26
tags: Softmax
categories: MachineLearning
---

> SVM只选自己喜欢的男神，Softmax把所有备胎全部拉出来评分，最后还归一化一下   -----王晨琛
<!--more-->
## 从名字上理解
上面一句话可谓是精辟，Softmax回归是[logistics回归](http://www.jianshu.com/p/4db93e9f38af)在多分类问题上的推广。max就是比较大小取大呗，但是有时不能直接取，不然会造成分值小的饥饿，怎么解决，也要雨露均沾，经常取大的，偶尔取小的就好了，概率和大小有关这也就是为啥是soft max。

Softmax回归具体的典型实例就是[MNIST手写数字分类(关于Softmax部分)](http://www.tensorfly.cn/tfdoc/tutorials/mnist_beginners.html)。

这个函数在[斯坦福最优化课程28分钟左右](https://www.youtube.com/watch?v=G4G7dWBi3II&list=PLbBM_dvjud8oFj09MqqYnGSrT6zek42Q0&index=4)有详细讲解，在吴恩达的课程中也有，不懂得可以再详细看看。

## 原理
Softmax代价函数与logistic 代价函数在形式上非常类似，只是在Softmax损失函数中对类标记的k个可能值进行了累加。注意在Softmax回归中将x分类为类别j的概率为：
![Softmax代价函数与logistic 代价函数在形式上非常类似](http://upload-images.jianshu.io/upload_images/744392-7ea9eb17fa574abe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
J(θ)最下化问题，通过求导得到梯度公式：
![梯度公式](http://upload-images.jianshu.io/upload_images/744392-841d57054be63449.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Softmax是有监督的，当然也可以和无监督结合用。这个后面文章再说，

简单的可以这样看：假设有一个数组V,Vi表示第i个指数，那么这个元素的Softmax值为：


![Softmax值：该元素指数与所有元素指数和之比](http://upload-images.jianshu.io/upload_images/744392-f938d5f1f6a9268b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 优点
 #### 1、计算与标注样本的差距
在神经网络计算中，我们经常计算正向传播计算分数S1和按照正确标注的分数S2之间的差距，计算Loss，才能应用反向传播。Loss定义为交叉熵

![L_{i} = -\log(\frac{e^{f_{y_{i}}}}{\sum_{j}e^{j}})](http://upload-images.jianshu.io/upload_images/744392-93c197dbc6d110f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

取log里面的值就是这组数据正确分类的Softmax值，它占的比重越大，这个样本的Loss也就越小，这种定义符合我们的要求

####  2、计算方便
当我们对分类的Loss进行改进的时候，我们要通过梯度下降，每次优化一个step大小的梯度，这个时候我们就要求Loss对每个权重矩阵的偏导，然后应用链式法则。那么这个过程的第一步，就是求Loss对score的偏导 (下面公式推导部分对于求偏导符号就用求导符号代替)


![推导](http://upload-images.jianshu.io/upload_images/744392-02d0f2e4fcd8015c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![直接结果](http://upload-images.jianshu.io/upload_images/744392-3035225fe2166829.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
最后结果的形式非常的简单，只要将算出来的概率的向量对应的真正结果的那一维减1，就可以了，举个例子，通过若干层的计算，最后得到的某个训练样本的向量的分数是[ 1, 5, 3 ], 那么概率分别就是[0.015,0.866,0.117],如果这个样本正确的分类是第二个的话，那么计算出来的偏导就是[0.015,0.866−1,0.117]=[0.015,−0.134,0.117]，是不是很简单！！然后再根据这个进行back propagation就可以了。





看完上面还懂吗，不懂看这幅图
![《一天搞懂深度学习》](http://upload-images.jianshu.io/upload_images/744392-144e8942fbf438f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


不行就推推公式看看视频反过来再看看,数学公式的详细推到在这里面[ufldl:Softmax回归](http://ufldl.stanford.edu/wiki/index.php/Softmax%E5%9B%9E%E5%BD%92)



