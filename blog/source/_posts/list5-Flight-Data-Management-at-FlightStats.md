---
title: list5-Flight Data Management at FlightStats
date: 2017-07-18 23:16:36
tags: Application
categories: BigData
---
这是在Coursera上课程中一个真实的例子，我想这个例子可以很直观让我们感受到大数据具体是怎么应用的。
<!--more-->后面讲的都是数据库或者Hadoop，Spark一点应用，可以在hand on看一下，再写出来就没有意义，所以就到此为止了。后面还是按照给自己定的学习计划进行，而且也通过半个月时间也了解机器学习在大数据下的应用，受益匪浅，值得了。
下面是演讲稿：

嗨，我叫乍得伯克利。我是FlightStats的首席技术官，我今天在这里与您谈谈我们的平台，以及我们如何获取和处理数据。但首先，我想首先介绍一下公司，并告诉你一些关于我们的事情。所以FlightStats是一家数据公司，我们基本上是全球实时航班状态数据的领先供应商。我们从500多个来源获取数据，我们将这些数据汇总在一起，我们将其出售给我们其他企业以及消费者的客户。

![image.png](http://upload-images.jianshu.io/upload_images/744392-76de31bd3d8be096.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


所以只是给你一些关于我们做什么的范围和规模的信息。就像我说的，我们有超过500个数据源。每天我们处理大约1500万次飞行事件，包括着陆，到达，离港。

随着航班状态的变化，我们得到了一些消息。我们每天处理约2.6亿飞机的位置，所以我们有一个广泛的网络，监视图表位置的实时航班跟踪应用程序。我们还处理大约一百万个PNR或乘客姓名记录，这是您在旅行任何时候旅行的实际数据类型，PNR是为您创建的，用于您的旅行。它包括所有的细分，如航空旅行，渡轮，酒店，出租车，可以安排在您的旅行的任何安排。而且我们基本上把所有的数据都收集起来，我们把它们汇总在一起，然后把它们退出来。大多数人都知道我们的FlightStats.com，这是我们的消费者网站的业务，我们处理约200万日常请求。我们处理大约100万个移动应用请求。


![image.png](http://upload-images.jianshu.io/upload_images/744392-02c7b2feb49bd4d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们的b2b ，我们通过API和实时数据Feed认证了大量数据。人们每天向我们提供约1500万个API请求。我们还发出了大约一百五十万次飞行和旅行通知。所以如果你的手机推送通知，告诉你你的航班延误或准时。这可能来自我们。那么一点关于数据如何流经我们公司。我们引入所有这些不同类型的数据和来源，并通过我们的数据采集团队。我们有一个团队，其主要目的是提取各种原始数据，一个非常异构的数据集。并将其处理为规范化形式。因此，如果您在本图中遵循蓝色箭头，您可以看到它通过数据中心通过这个原始数据通道。哪个数据中心是我们系统的核心部件，我将在稍后再说一遍。所以蓝色数据，蓝线是从源头进入的原始数据通过我们的数据采集系统，它变成了一个标准化形式的紫色线。然后再次通过我们的数据中心进入我们的处理引擎。我们的处理引擎真的是大多数业务逻辑发生的地方。我们必须做的第一件事是，我们必须根据我们所知道的航班匹配任何航班信息，主要是通过航班了解航班的方式。所以我们每天从我们的合作伙伴计划供应商中导入日程表。

一旦匹配的数据被处理，并且处理基本上看每个消息，并尝试确定我们认为该消息是否需要传递给消费者。所以你知道它看起来像我们以前看过的消息。还是重复？是从我们信任的数据源吗？

还有其他的事情，我们需要知道的可能会影响是否该消息是真的？一旦我们决定通过消息，如果你遵循绿线。它进入我们的中心的过程数据通道，然后被推出到几个不同的地方。首先，它进入我们的生产数据库，这是我们所有的实时数据的生命。该数据库为我们的网站，移动应用程序和其他各种场所提供数据。它也进入我们的数据仓库，这是我们的分析产品使用它的地方。我会在稍后再说一遍。然后，数据流实际上上升到了我们很多客户。我们不需要我们这边的数据库。他们宁愿在他们身边建立一个数据库，所以我们实际上只是将所有处理的数据直接传递给他们。然后他们将其托管在自己的系统中。

所以更多关于中枢，中心是我们如何移动数据的核心。这是我们内部开发的一种技术。它是一种基于对象存储的，可扩展的，高可用性的多通道数据排队和事件系统。对象存储部分是，我们使用Amazon S3存储这些数据。所以这是一个对象存储系统。它是可扩展的，我们可以水平或垂直放大，取决于，但是什么类型的数据流经它。这是非常有意义的，我们在不同的数据中心有多个实例。所以如果一个下降我们可以轻松地拉另一个，或者我们将要跨越多个实例。然后是多频道。所以它有一个休息界面，任何表面都可以在系统内创建一个新的通道，并开始向其发布数据。然后，该数据根据进入的时间排队，其他服务可以在这些频道上监听事件。因此，一旦新的数据进入其中一个频道，任何在该频道上侦听的服务就会收到一个事件通知。他们，那个服务然后可以对这条数据行事。并做任何可能需要做的处理。这个项目是开源的，任何人都可以下载并使用它。

![image.png](http://upload-images.jianshu.io/upload_images/744392-8902c8bee635ebc0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


那么一点点关于我们收集和汇总的一些数据。 FLIFO是飞行信息的行业术语。主要是看飞机的五个不同部分。所以我们拉闸门出发的信息，然后就成为跑道离开，基本上当车轮上升时，就是跑道离开。我们进行飞行中的位置跟踪，所以当你的航班正在移动时，大约每十秒钟一次，我们会收到其纬度和经度的通知。其标题及其速度及其垂直中心下降率等几个变量。

一旦它落地，一旦轮子碰到地面，我们被通知跑道到达，当门在门口打开时，我们有门到达信息。所有这五个数据字段有三种不同的形式。所以我们有一个预定的，定期的出发和到达。我们估计出发和到达可能来自各种来源，包括航空公司，机场，位置数据等。那么，如果我们有一个机场或一家航空公司向我们发送关于车轮碰到的准确数据的准确情况，或正好在那个车门打开的时候，我们也有实际的意见，我们也推送这些数据。我们还在航班停止时生成一些数据。那么特殊的事情，如果一架飞机有一个问题在消息。我们通过我们的支持人员的信息标记我们的内容。我们做一些预测现在我们刚刚开始进入这个市场，或者我们实际上是在24小时内预测航班是否会被延迟，中断或及时。

我们做一些合成的职位，主要是在海洋上。我们没有在海洋上获取飞机上的跟踪数据。目前还没有基于卫星的飞机跟踪系统。所以我们基本上以最后一个已知的位置为标题，速度。如果我们有一个飞行计划，我们将使用飞行计划来综合这些位置，当我们没有在大型水域上获得实际的职位。我们还生成通知，所以推送警报，预检电子邮件，延迟通知这些类型的事情。我们根据我们所看到的数据创建这些数据。我们将所有的历史数据存储在数据仓库中，所以现在我们有六年历史的航班数据。这使我们的分析产品成为可能，所以我们允许航空公司进行竞争分析和路线分析。

![image.png](http://upload-images.jianshu.io/upload_images/744392-9784eb211c1f00dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


路线对航空公司非常重要。这就是他们如何相互竞争，主要是由FAA和其他政府机构判断他们是否准时。我们也做机场运营分析的事情，比如出租车和出租车时间。对于许多机场，跑道利用率，通过机场的小时乘客来说，这种类型的信息非常重要。而且我们也按时执行性能指标。航空公司可以看看他们在做什么。他们完成了多少班航机？ 14分钟内有多少班机次？

他们可以将自己与竞争对手进行比较。所以我们在混合云架构中主持所有这些。混合云基本上意味着我们拥有自己的私有数据中心资源，我们还在Amazon Web Services云中托管资源。

![image.png](http://upload-images.jianshu.io/upload_images/744392-a6c3dd5f1719fd55.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们的大多数核心数据处理和服务层都在我们的私人数据中心，我们也准备好再次启动第二个私人数据中心。现在，我们的主要数据中心位于俄勒冈州的波特兰，我们将在第二季度或第三季度在美国东海岸再转一个。对于我们的API，我们试图让这些API靠近我们的客户，所以API终点和Web终点都存在于亚马逊。并且它们会自动路由到最接近您的终点，您将自动路由到它们。

我们所有的私有基础设施都通过VMWare虚拟化。我们几乎都有一个完全虚拟化的环境。而我们是一个敏捷商店，所以我们有六个小而快速的团队。那些是以产品为中心的团队，我们允许他们像他们所需要的一样是客户互动，我们试图使我们的团队半自治。所以，团队选择自己的工具，他们选择自己的开发方法，他们选择各种各样的东西。而且我们实际上允许他们尽可能快地完成他们所需要做的工作。

![image.png](http://upload-images.jianshu.io/upload_images/744392-8a468669a53d45de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们尝试自动化一切。您手动执行某些操作，然后在下次编写脚本或程序时执行此操作。而且我们也测量一切。现在，我们每个月从系统中获取约25亿个指标。而且我们使用这些指标监控我们的应用程序性能，监控收入，几乎监控我们在公司所做的一切。我们真的尝试启用全面的系统意识，从硬件层到网站的所有内容都被监控。

我们使用行业最佳实践和工具，当然，我们试图招募和聘请最有可能的人才，了解我们的软件库存。我们主要是一个Java商店。

![image.png](http://upload-images.jianshu.io/upload_images/744392-c8eb55921283ff59.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们的核心处理服务都是用Java编写的。我们在我们的微服务边缘层中使用节点JS。而节点JS实际上也开始进一步向下进入处理服务层。我们使用许多不同类型的数据库。我们的主要实时数据库是Post Press。而我们使用Mongo作为我们的API服务的后端。

在网站上，我们都是HTML5，我们正在转向React和Redux，我们正在使用Elasticsearch快速搜索和索引我们的数据。而且，我们当然有iOS和Android移动应用。所以你可以在我们的网站上找到关于Flightstats的更多信息。如果您需要应用程序的数据，请访问developer.flightstats.com的开发人员中心。您可以注册一个免费的测试帐户，并能够直接从我们的API中提取数据。如果你对Hub有兴趣，就像我说的那样，这是开源的。请查看Git Hub页面，如果您有任何其他问题，请随时与John Berkeley联系，我很乐意通过电子邮件回答您的任何问题。感谢今天听，希望你有一个美好的一天。再见。

[原视频地址](https://www.coursera.org/learn/big-data-management/lecture/ITqCN/flight-data-management-at-flightstats-a-lecture-by-cto-chad-berkley)

