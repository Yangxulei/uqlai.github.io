---
title: list2-Running HelloWorld on Hadoop
date: 2017-07-11 08:25:15
tags: WordCount
categories: BigData
---
上次笔记讲了关于大数据的基本内容和文章末尾给了配置Cloudera的教程，这次了解Hadoop文件系统或HDFS的基本文件操作命令。我们先从下载[text文件](https://ocw.mit.edu/ans7870/6/6.006/s08/lecturenotes/files/t8.shakespeare.txt)开始。我们将使用这个text文件来复制HDFS中的本地文件系统，并使用它来运行word count
<!--more-->
#1、 Copy your data into the Hadoop Distributed File System

下载文本文件后，我们将在Cloudera打开一个终端shell，并将文本文件从本地文件系统复制到HDFS。
![image.png](http://upload-images.jianshu.io/upload_images/744392-b634a4ed9c6e11c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来，我们将复制HDFS中的文件，还可以看到如何将文件从HDFS复制到本地文件系统。最后，我们将看看如何在HDFS中删除文件。

#### 一、复制
让我们将word.txt从本地文件系统复制到HDFS文件系统:

```
hadoop fs- copyFromLocal words.txt。
```

当我运行它，它会将其从本地目录和本地文件系统复制到HDFS。

接下来，我们可以将此文件复制到HDFS中的另一个文件。我们可以通过运行
```
hadoop fs -cp words.txt words2.txt
```
#### 二、查看
```
hadoop fs -ls
``` 
来查看存在的文件,可以在下图中看到第一个word.txt是HDFS中已经存在的文件。第二个word2.txt是我们运行此命令时要创建的新文件。


![image.png](http://upload-images.jianshu.io/upload_images/744392-fb2b0ff94cfc63f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们来将word2.txt从HDFS复制到本地文件系统。我们可以通过运行
```
hadoop fs -copyToLocal word2.txt来执行此操作。
```

运行此命令后，我可以调用ls来查看本地文件系统的内容。所以现在我们有刚刚从HDFS复制的新文件word2.txt。
#### 三、删除HDFS文件
我们可以通过运行
```
hadoop fs -rm words2.txt
```


![image.png](http://upload-images.jianshu.io/upload_images/744392-109d0a915460b4e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

来删除words2.txt,你可以看到它打印出它删除了该文件。我们也可以运行hadoop fs -l来验证文件是否被删除。

# 2、Run the WordCount program Instructions

这个例子使用Hadoop来运行WordCount，这是入门几乎都会做的“hello world”吧。

首先我们将打开一个终端shell并探索Hadoop提供的MapReduce程序，接下来验证HDFS中存在的输入文件。然后，运行WordCount并浏览WordCount输出目录，我们将WordCount的结果从HDFS复制到本地文件系统并查看，这就是这个例子的流程了。code起来~~


接下来，我们将看看生成的Hadoop程序。我们可以运行
```
$Hadoop jar usr/jar/Hadoop-examples.jar ```

这个命令说明我们将使用jar命令从jar文件中在Hadoop中运行一个程序。而我们正在运行的jar文件位于/usr/jars/hadoop-examples.jar中。许多使用Java编写的程序通过jar文件进行分发。如果我们运行这个命令，我们将看到Hadoop附带的不同程序的列表。所以例如wordcount。计算文本文件中的单词。Wordmean，计算单词的平均长度。和其他程序，如排序和计算pi的长度。

![image.png](http://upload-images.jianshu.io/upload_images/744392-e101358d28701d22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
hadoop jar /usr/jars/hadoop-examples.jar wordcount```
是说说，我们要运行一个jar，这是包含程序的jar的名字。而我们要运行的程序是wordcount。当我们运行它，我们看到它print命令行用法如何运行字数。这表示wordcount需要一个或多个输入文件和输出名称。现在，输入和输出均位于HDFS中。所以我们在HDFS中有刚刚列出的输入文件word.txt。我们可以运行wordcount。
```
 hadoop jar / usr / jars / hadoop-examples.jar wordcount words.txt```

这就是说，我们将使用word.txt作为输入运行WordCount程序，并将输出放在一个名为out的目录中。run起来随着字数运行，print到屏幕。它将print，map的百分比并缩小完成。而当两者达到100％时，就完成了这项工作。

![image.png](http://upload-images.jianshu.io/upload_images/744392-8a6da7faea9e6fe8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们通过运行```Hadoop fs -ls out```来查看输出结果的目录。 [BLANK AUDIO]我们可以看到目录中有两个文件。第一个是_SUCCESS，这意味着WordCount作业成功完成。

![image.png](http://upload-images.jianshu.io/upload_images/744392-dd066963fa12f13a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

另一个文件-r-00000是包含WordCount命令输出的文本文件，现在我们可以通过运行```hadoop fs -copytolocal out / part-r-00000 loacl.txt```从HDFS将这个文本文件复制到本地文件系统，然后查看它。

我们在此文件中看到WordCount的结果。每行是一个特定的单词，第二列是在输入文件中找到该特定单词的单词数。

![image.png](http://upload-images.jianshu.io/upload_images/744392-9819e482394066ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[](https://www.coursera.org/learn/big-data-introduction/supplement/HIcQh/how-do-i-figure-out-how-to-run-hadoop-mapreduce-programs)

