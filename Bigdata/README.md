#Everything about Big data

###Apache Spark
>####Spark概览
>key word: [IBM 上关于Spark实战的案例](http://www.ibm.com/search/csass/search/?q=spark%2B%E5%AE%9E%E6%88%98%2B%E7%8E%8B%E9%BE%99&dws=cndw&ibm-search.x=-655&ibm-search.y=-329&ibm-search=Search&sn=dw&lang=zh&cc=CN&ddr=&en=utf&lo=zh&hpp=20)
>
>Spark 是一个通用的大规模数据快速处理引擎。可以简单理解为 Spark 就是一个大数据分布式处理框架，主要特点是提供了一个集群的分布式内存抽象，以支持需要工作集的应用。

>Spark是基于map reduce算法实现的分布式计算框架，但不同的是Spark的中间输出和结果输出可以保存在内存中，从而不再需要读写HDFS，因此Spark能更好地用于数据挖掘与机器学习等需要迭代的map reduce的算法中。
>Spark 架构如下图：
>![image](http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/bdas.jpg)

>分布式内存抽象，就是RDD（Resilient Distributed Dataset），RDD就是一个不可变的带分区的记录集合，RDD也是Spark中的编程模型。Spark提供了RDD上的两类操作，转换和动作。转换是用来定义一个新的RDD，包括map, flatMap, filter, union, sample, join, groupByKey, cogroup, ReduceByKey, cros, sortByKey, mapValues等，动作是返回一个结果，包括collect, reduce, count, save, lookupKey。

>Spark的API非常简单易用，Spark的WordCount的示例如下所示（scala实现）：
```scala
val spark = new SparkContext(master, appName, [sparkHome], [jars])
val file = spark.textFile("hdfs://...")
val counts = file.flatMap(line => line.split(" "))
                 .map(word => (word, 1))
                 .reduceByKey(_ + _)
counts.saveAsTextFile("hdfs://...")
```
>其中的file是根据HDFS上的文件创建的RDD，后面的flatMap，map，reduceByKe都创建出一个新的RDD，一个简短的程序就能够执行很多个转换和动作。

### Hadoop

>Hadoop就是解决了大数据（大到一台计算机无法进行存储，一台计算机无法在要求的时间内进行处理）的可靠存储和处理。
>Hadoop实现以下分布式存储和计算模型：
>
>HDFS，在由普通PC组成的集群上提供高可靠的文件存储，通过将块保存多个副本的办法解决服务器或硬盘坏掉的问题。

>MapReduce，通过简单的Mapper和Reducer的抽象提供一个编程模型（然而计算的细节需要工程人员自己实现），可以在一个由几十台上百台的PC组成的不可靠集群上并发地，分布式地处理大量的数据集，而把并发、分布式（如机器间通信）和故障恢复等计算细节隐藏起来。而Mapper和Reducer的抽象，又是各种各样的复杂数据处理都可以分解为的基本元素。这样，复杂的数据处理可以分解为由多个Job（包含一个Mapper和一个Reducer）组成的有向无环图（DAG）,然后每个Mapper和Reducer放到Hadoop集群上执行，就可以得出结果。

>####Hadoop的局限和不足

>1. 抽象层次低，需要手工编写代码来完成，使用上难以上手。
2. 只提供两个操作，Map和Reduce，表达力欠缺。
3. 一个Job只有Map和Reduce两个阶段（Phase），复杂的计算需要大量的Job完成，Job之间的依赖关系是由开发者自己管理的。
4. 处理逻辑隐藏在代码细节中，没有整体逻辑
5. 中间结果也放在HDFS文件系统中
6. ReduceTask需要等待所有MapTask都完成后才可以开始
7. 时延高，只适用Batch数据处理，对于交互式数据处理，实时数据处理的支持不够
8. 对于迭代式数据处理性能比较差

>不过也有许多技术对Hadoop进行改进，如```Pig```，```Cascading```，```JAQL```，```OOzie```，```Tez```，```Spark```等。

##Benchmark
>Spark的性能相比Hadoop有很大提升，2014年10月，Spark完成了一个Daytona Gray类别的Sort Benchmark测试，排序完全是在磁盘上进行的，与Hadoop之前的测试的对比结果如表格所示：
![image](https://pic2.zhimg.com/029ab6e670fa8f5248d5120ab5fb3a59_b.jpg)


>来源：［https://www.zhihu.com/question/26568496］

##总结
作者：用心阁
链接：https://www.zhihu.com/question/26568496/answer/41608400
来源：知乎
著作权归作者所有，转载请联系作者获得授权。

那么Spark解决了Hadoop的哪些问题呢？
1. 抽象层次低，需要手工编写代码来完成，使用上难以上手。
=>基于RDD的抽象，实数据处理逻辑的代码非常简短。。
2. 只提供两个操作，Map和Reduce，表达力欠缺。
=>提供很多转换和动作，很多基本操作如Join，GroupBy已经在RDD转换和动作中实现。
3. 一个Job只有Map和Reduce两个阶段（Phase），复杂的计算需要大量的Job完成，Job之间的依赖关系是由开发者自己管理的。
=>一个Job可以包含RDD的多个转换操作，在调度时可以生成多个阶段（Stage），而且如果多个map操作的RDD的分区不变，是可以放在同一个Task中进行。
4. 处理逻辑隐藏在代码细节中，没有整体逻辑
=>在Scala中，通过匿名函数和高阶函数，RDD的转换支持流式API，可以5. 提供处理逻辑的整体视图。代码不包含具体操作的实现细节，逻辑更清晰。
6. 中间结果也放在HDFS文件系统中
=>中间结果放在内存中，内存放不下了会写入本地磁盘，而不是HDFS。
7. ReduceTask需要等待所有MapTask都完成后才可以开始
=> 分区相同的转换构成流水线放在一个Task中运行，分区不同的转换需要Shuffle，被划分到不同的Stage中，需要等待前面的Stage完成后才可以开始。
8. 时延高，只适用Batch数据处理，对于交互式数据处理，实时数据处理的支持不够
=>通过将流拆成小的batch提供Discretized Stream处理流数据。
9. 对于迭代式数据处理性能比较差
=>通过在内存中缓存数据，提高迭代式计算的性能。

[^scala]:Scala 语言是一门类 Java 的多范式语言，其设计初衷就是为了继承函数式编程的面向对象编程的各种特性，正如 Scala 语言官网 描述的那样:Object-Oriented Meets Functional, 就是给出了一个关于 Scala 语言特性的最简单明了的概括。
Spark 框架使用 Scala 语言开发，那么使用 Scala 语言开发 Spark 应用程序就变成一件很自然的事情，虽然 Spark 提供了面向 Python,Java 等语言的编程接口，但是从各个方面来看使用 Scala 编程都是最简单最容易理解的，特别是当程序出现异常或者是需要通过学习源码来定位问题时，您会发现学习 Scala 语言来编写 Spark 应用程序是多么有意义的事情。




