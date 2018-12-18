---
title: RE与FA(上)
date: 2018-04-03 21:12:08
tags: 自动机
---


![词法分析器的自动生成方法](https://upload-images.jianshu.io/upload_images/744392-eb349b9f87c37fc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
程序员只需要指定声明式的规范就行，不需要书写繁重复杂的词法分析器算法，大大减少了工作量。

#  正则表达式
- 对给定的字符集 Σ = c1,c2,....cn.
- 正则表达式是一个声明式的规范方法
    - 归纳定义：
    - 空串ε 是正则表达式
    - 对于任意的 c ∈  Σ， c是正则表达式
    - 如果M和N是正则表达式，则下面也是正则表达式
        - 选择： M | N  = {M, N}
        - 连接： MN = {mn | m ∈ M, n ∈ N}
        - 闭包： M* = {ε, M, MM, MMM, ...}  (Kleene 闭包)

如下是正则表达式的形式表示：
![正则例子](https://upload-images.jianshu.io/upload_images/744392-99341eeef078ba65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此中前面的两种是基本形式，后面三种是归纳形式，选择，连接和闭包。

对于给定的一个字符集 Σ = a,b 可以写出如下正则表达式
- 1、ε 
- 2、a, b
- 3、ε | ε  ......(选择)
- 4、ε a, ε b, ab,ε ε , ....., a(ε | a),....... （连接）
- 5、ε *，(a(ε |a))*，...... (闭包)


 可以写出如下正则表达式：

1.  ε （第一个规则，空串ε是正则表达式）
2.  a, b
3.  ε|ε， ε|a，... （选择）
4.  εa， εb， ab， εε， ..., a(ε|a), ... （连接）
5.  ε*, (a(ε|a))*, ... （闭包）

C语言中有很多关键字，例如 if, while 等：

对于 if ， i ∈ Σ， f ∈ Σ， 所以 if 属于正则表达式。
其他，同理。
C语言中的标识符，是以字母和下划线开头，后跟零个或者多个字母、数字或下划线。其用正则表达式表达的方式如下：(a|b|...|z|A|B|...|Z|_)(a|b|...|z|A|B|...|Z|_|0|1|...|9)*。因为这里的后面部分是可以为零的，也就是任意个，所以直接使用闭包即可。

## 语法糖
可以引入更多的语法糖，来简化创造。
- [c1 - cn] == c1|c2|c3|...|cn
- e+ == 一个或者多个e
- e? ==  零个或一个e， 等价于 ε | e
-"a*" == a* 本身，不是 a 的 Kleen 闭包
- e{i,j} == i 到j个e的连接
- . == 除'\n'外的任意字符

ps：汇编是通过赋值与跳转两种就可以完成所有的机制，通过语法糖可以封装高效利用这些机制


# 有限自动机
[JavaScript与有限状态机](http://www.ruanyifeng.com/blog/2013/09/finite-state_machine_for_javascript.html)
从上述例子更好理解状态转移
![词法分析器的自动生成方法](https://upload-images.jianshu.io/upload_images/744392-eb349b9f87c37fc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 输出更加形式化的表达：有限状态自动机
![有限自动机](https://upload-images.jianshu.io/upload_images/744392-b58e5b2999cfbca5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 确定有限自动机（DFA）
- 对任意的字符，最多有一个状态可以转移
    - δ： S * Σ -> S

例子：

![确定有限自动机](https://upload-images.jianshu.io/upload_images/744392-e4048eda56858566.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- Σ 表示自动机可以识别的所有的不同的字符的集合。 Σ = {a, b}
- S 是状态集，在这里只有三种状态，所以 S = {0, 1, 2}
- q0 是初始状态，我们一般约定只有一个单向箭头的边指向的节点是起始状态。q0 = 0
- F 是终结状态，或者说是接收状态，在图中表示为双圈。 F = {2}
- δ 是转移函数，是一个映射的概念，为 

{(q0, a) -> q1, (q0, b) -> q0, 
(q1, a) -> q2, (q1, b) -> q1,
(q2, a) -> q2, (q2, b) -> q2}。 是所有的映射构成的一个集合。

#### 串被接受？
接受的意思就是处于起始状态，给定一个输入串S，根据转移函数δ进行状态转移，最后到达了F总结状态，这样的串S就可以被接受。
# 非确定有限自动机 （NFA）

- 对任意的字符，有多余一个状态可以转移
  -  δ：S X (Σ ∪ ε) -> Φ(S的幂集)

ps： X：笛卡尔积
  eg: s={a,b}  幂集={φ，{a},{b},{a,b}} 共有2^n
   

![非确定有限自动机例子](https://upload-images.jianshu.io/upload_images/744392-bb090a603ef48cd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
转移函数：
{(q0, a) -> {q0, q1},       // 得到一个集合
(q0, b) -> {q1},
(q1, b) -> {q0, q1}}     //得到一个集合

综上例子来种自动机，对于存在一种状态 ，给定的一个字符的转移函数是不确定，可以得到一个集合，如上式中的第一个和第三个集合，我们称这样的状态机是非确定状态自动机（NFA）。如果转移函数所有的结果都是一个确定的值，是单集合元素，就像上一个例子一样，这样的状态机就是确实有限状态自动机（DFA）。
#### 对于 NFA 和 DFA 在接受的时候有很大的差别。
如该例中，q0 状态在 a 状态后可以得到 q0 或 q1 两种状态，如果是 q0 那就不能进入终结状态F，不能被接受，而选择 q1 时可以被接受。所以我们对 NFA 定义，只要在多种走法中最终由一种走法可以被接受就是可以被接受。所以该例可以被接受。

一般对于这种是否可以接受的判断，我们常常会先将 NFA 转化为 DFA 再进行判断。

## DFA实现：
DFA其实是一个有向图，可以用邻接矩阵对其进行了表示。



*！！！！对于ε动作的FA会放在下面一块讲解*
# 正则表达式到非确定有限状态自动机的转化算法
![image.png](https://upload-images.jianshu.io/upload_images/744392-cf0bb874214ef43c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- RE->NFA ：[Thompson算法](https://zh.wikipedia.org/wiki/Thompson%E6%9E%84%E9%80%A0%E6%B3%95)(递归)
- NFA->DFA：子集构造算法
- DFA->: 词法分析器代码：使用 Hopcroft 最小化算法做压缩。

#### [Thompson算法](https://zh.wikipedia.org/wiki/Thompson%E6%9E%84%E9%80%A0%E6%B3%95)

- 基于对 RE 的结构做归纳
   - 对基本的 RE 直接构造
   - 对复合的 RE 递归构造
- 递归算法，容易实现

举个栗子🌰：

![image.png](https://upload-images.jianshu.io/upload_images/744392-4d22655baf72ac72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 对于第一种空串和第二种一个单个字符，可以直接构造

![e->ε](https://upload-images.jianshu.io/upload_images/744392-912c568363bc5a5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![e->c](https://upload-images.jianshu.io/upload_images/744392-793cc18da0a62a34.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 后三种可以通过递归构造

![e -> e1e2](https://upload-images.jianshu.io/upload_images/744392-7181f8d7f00531c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![e -> e1 | e2](https://upload-images.jianshu.io/upload_images/744392-77aa07da573a92fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![e -> e1*](https://upload-images.jianshu.io/upload_images/744392-efe5aa07b016c2b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 看一个复杂点的例子，(a|b)*abb，它所对应的 NFA 如下：
![课本28页](https://upload-images.jianshu.io/upload_images/744392-18af4fda4dfc8cdb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)




# 推荐阅读:
[手把手教你构建 C 语言编译器](http://lotabout.me/2015/write-a-C-interpreter-0/)

# Reference：
- 《编译原理》(龙书)
- [DFA&NFA（简易比较）](https://blog.csdn.net/echo_qiang/article/details/5904563)
- [Web中无处不在的状态机](https://zhuanlan.zhihu.com/p/26524390)











