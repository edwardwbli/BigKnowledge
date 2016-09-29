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
>
>Spark生态系统BDAS
>
（1）Spark

>Spark是整个BDAS的核心组件，是一个大数据分布式编程框架，不仅实现了MapReduce的算子map 函数和reduce函数及计算模型，还提供更为丰富的算子，如filter、join、groupByKey等。Spark将分布式数据抽象为弹性分布式数据集（RDD），实现了应用任务调度、RPC、序列化和压缩，并为运行在其上的上层组件提供API。其底层采用Scala这种函数式语言书写而成，并且所提供的API深度借鉴Scala函数式的编程思想，提供与Scala类似的编程接口。图1-2为Spark的处理流程（主要对象为RDD）。

>Spark将数据在分布式环境下分区，然后将作业转化为有向无环图（DAG），并分阶段进行DAG的调度和任务的分布式并行处理。

>（2）Shark

>Shark是构建在Spark和Hive基础之上的数据仓库。目前，Shark已经完成学术使命，终止开发，但其架构和原理仍具有借鉴意义。它提供了能够查询Hive中所存储数据的一套SQL接口，兼容现有的Hive QL语法。这样，熟悉Hive QL或者SQL的用户可以基于Shark进行快速的Ad-Hoc、Reporting等类型的SQL查询。Shark底层复用Hive的解析器、优化器以及元数据存储和序列化接口。Shark会将Hive QL编译转化为一组Spark任务，进行分布式运算。

>（3）Spark SQL

>Spark SQL提供在大数据上的SQL查询功能，类似于Shark在整个生态系统的角色，它们可以统称为SQL on Spark。之前，Shark的查询编译和优化器依赖于Hive，使得Shark不得不维护一套Hive分支，而Spark SQL使用Catalyst做查询解析和优化器，并在底层使用Spark作为执行引擎实现SQL 的Operator。用户可以在Spark上直接书写SQL，相当于为Spark扩充了一套SQL算子，这无疑更加丰富了Spark的算子和功能，同时Spark SQL不断兼容不同的持久化存储（如HDFS、Hive等），为其发展奠定广阔的空间。

>（4）Spark Streaming

>Spark Streaming通过将流数据按指定时间片累积为RDD，然后将每个RDD进行批处理，进而实现大规模的流数据处理。其吞吐量能够超越现有主流流处理框架Storm，并提供丰富的API用于流数据计算。

>（5）GraphX

>GraphX基于BSP模型，在Spark之上封装类似Pregel的接口，进行大规模同步全局的图计算，尤其是当用户进行多轮迭代时，基于Spark内存计算的优势尤为明显。

>（6）Tachyon

>Tachyon是一个分布式内存文件系统，可以理解为内存中的HDFS。为了提供更高的性能，将数据存储剥离Java Heap。用户可以基于Tachyon实现RDD或者文件的跨应用共享，并提供高容错机制，保证数据的可靠性。

>（7）Mesos

>Mesos是一个资源管理框架，提供类似于YARN的功能。用户可以在其中插件式地运行Spark、MapReduce、Tez等计算框架的任务。Mesos会对资源和任务进行隔离，并实现高效的资源任务调度。

>（8）BlinkDB

>BlinkDB是一个用于在海量数据上进行交互式 SQL 的近似查询引擎。它允许用户通过在查询准确性和查询响应时间之间做出权衡，完成近似查询。其数据的精度被控制在允许的误差范围内。为了达到这个目标，BlinkDB的核心思想是：通过一个自适应优化框架，随着时间的推移，从原始数据建立并维护一组多维样本；通过一个动态样本选择策略，选择一个适当大小的示例，然后基于查询的准确性和响应时间满足用户查询需求。

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




