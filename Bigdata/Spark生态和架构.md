<div id="main" class="post" itemscope="" itemprop="blogPost">
	<article itemprop="articleBody">
		<header class="article-info clearfix">
  <h1 itemprop="name">
    
      <a href="/2015/06/07/Spark/【Spark】Spark生态和Spark架构/" title="【Spark】Spark生态和Spark架构" itemprop="url">【Spark】Spark生态和Spark架构</a>
  </h1>
  <p class="article-author">By
    
      <a href="http://blog.jasonding.top" title="Jason Ding">Jason Ding</a>
    </p>
  <p class="article-time">
    <time datetime="2015-06-07T07:46:37.000Z" itemprop="datePublished">2015-06-07</time>
    Updated:<time datetime="2016-03-16T06:24:42.000Z" itemprop="dateModified">2016-03-16</time>
    
  </p>


		
		<h2 id="Spark概览"><a href="#Spark概览" class="headerlink" title="Spark概览"></a>Spark概览</h2><p>Spark 是一个通用的大规模数据快速处理引擎。可以简单理解为 Spark 就是一个大数据分布式处理框架。<br><strong>Spark是基于map reduce算法实现的分布式计算框架，但不同的是Spark的中间输出和结果输出可以保存在内存中，从而不再需要读写HDFS，因此Spark能更好地用于数据挖掘与机器学习等需要迭代的map reduce的算法中。</strong></p>
<h2 id="Spark生态系统BDAS"><a href="#Spark生态系统BDAS" class="headerlink" title="Spark生态系统BDAS"></a>Spark生态系统BDAS</h2><p>伯克利将Spark的整个生态系统称为伯克利数据分析栈(BDAS)。其核心框架是Spark，同时BDAS涵盖支持结构化数据SQL查询与分析的查询引擎Spark SQL，提供机器学习功能的系统MLbase及底层的分布式机器学习库MLlib、并行图计算框架GraphX，流计算框架Spark Streaming、采样近似计算查询引擎BlinkDB、内存分布式文件系统Tachyon、资源管理框架Mesos等子项目。这些子项目在Spark上层提供了更高层、更丰富的计算范式。<br><img src="http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/bdas.jpg" alt=""></p>
<h3 id="（1）Spark"><a href="#（1）Spark" class="headerlink" title="（1）Spark"></a>（1）Spark</h3><p>Spark是整个BDAS的核心组件，是一个大数据分布式编程框架，不仅实现了MapReduce的算子map 函数和reduce函数及计算模型，还提供更为丰富的算子，如filter、join、groupByKey等。Spark将分布式数据抽象为弹性分布式数据集（RDD），实现了应用任务调度、RPC、序列化和压缩，并为运行在其上的上层组件提供API。其底层采用Scala这种函数式语言书写而成，并且所提供的API深度借鉴Scala函数式的编程思想，提供与Scala类似的编程接口。图1-2为Spark的处理流程（主要对象为RDD）。</p>
<p>Spark将数据在分布式环境下分区，然后将作业转化为有向无环图（DAG），并分阶段进行DAG的调度和任务的分布式并行处理。</p>
<h3 id="（2）Shark"><a href="#（2）Shark" class="headerlink" title="（2）Shark"></a>（2）Shark</h3><p>Shark是构建在Spark和Hive基础之上的数据仓库。目前，Shark已经完成学术使命，终止开发，但其架构和原理仍具有借鉴意义。它提供了能够查询Hive中所存储数据的一套SQL接口，兼容现有的Hive QL语法。这样，熟悉Hive QL或者SQL的用户可以基于Shark进行快速的Ad-Hoc、Reporting等类型的SQL查询。Shark底层复用Hive的解析器、优化器以及元数据存储和序列化接口。Shark会将Hive QL编译转化为一组Spark任务，进行分布式运算。</p>
<h3 id="（3）Spark-SQL"><a href="#（3）Spark-SQL" class="headerlink" title="（3）Spark SQL"></a>（3）Spark SQL</h3><p>Spark SQL提供在大数据上的SQL查询功能，类似于Shark在整个生态系统的角色，它们可以统称为SQL on Spark。之前，Shark的查询编译和优化器依赖于Hive，使得Shark不得不维护一套Hive分支，而Spark SQL使用Catalyst做查询解析和优化器，并在底层使用Spark作为执行引擎实现SQL 的Operator。用户可以在Spark上直接书写SQL，相当于为Spark扩充了一套SQL算子，这无疑更加丰富了Spark的算子和功能，同时Spark SQL不断兼容不同的持久化存储（如HDFS、Hive等），为其发展奠定广阔的空间。</p>
<h3 id="（4）Spark-Streaming"><a href="#（4）Spark-Streaming" class="headerlink" title="（4）Spark Streaming"></a>（4）Spark Streaming</h3><p>Spark Streaming通过将流数据按指定时间片累积为RDD，然后将每个RDD进行批处理，进而实现大规模的流数据处理。其吞吐量能够超越现有主流流处理框架Storm，并提供丰富的API用于流数据计算。</p>
<h3 id="（5）GraphX"><a href="#（5）GraphX" class="headerlink" title="（5）GraphX"></a>（5）GraphX</h3><p>GraphX基于BSP模型，在Spark之上封装类似Pregel的接口，进行大规模同步全局的图计算，尤其是当用户进行多轮迭代时，基于Spark内存计算的优势尤为明显。</p>
<h3 id="（6）Tachyon"><a href="#（6）Tachyon" class="headerlink" title="（6）Tachyon"></a>（6）Tachyon</h3><p>Tachyon是一个分布式内存文件系统，可以理解为内存中的HDFS。为了提供更高的性能，将数据存储剥离Java Heap。用户可以基于Tachyon实现RDD或者文件的跨应用共享，并提供高容错机制，保证数据的可靠性。</p>
<h3 id="（7）Mesos"><a href="#（7）Mesos" class="headerlink" title="（7）Mesos"></a>（7）Mesos</h3><p>Mesos是一个资源管理框架，提供类似于YARN的功能。用户可以在其中插件式地运行Spark、MapReduce、Tez等计算框架的任务。Mesos会对资源和任务进行隔离，并实现高效的资源任务调度。</p>
<h3 id="（8）BlinkDB"><a href="#（8）BlinkDB" class="headerlink" title="（8）BlinkDB"></a>（8）BlinkDB</h3><p>BlinkDB是一个用于在海量数据上进行交互式 SQL 的近似查询引擎。它允许用户通过在查询准确性和查询响应时间之间做出权衡，完成近似查询。其数据的精度被控制在允许的误差范围内。为了达到这个目标，BlinkDB的核心思想是：通过一个自适应优化框架，随着时间的推移，从原始数据建立并维护一组多维样本；通过一个动态样本选择策略，选择一个适当大小的示例，然后基于查询的准确性和响应时间满足用户查询需求。</p>
<h2 id="Spark的依赖"><a href="#Spark的依赖" class="headerlink" title="Spark的依赖"></a>Spark的依赖</h2><p><strong>（1）Map Reduce模型</strong><br>作为一个分布式计算框架，Spark采用了MapReduce模型。在它身上，Google的Map Reduce和Hadoop的痕迹很重，很明显，它并非一个大的创新，而是微创新。在基础理念不变的前提下，它借鉴，模仿并依赖了先辈，加入了一点改进，极大的提升了MapReduce的效率。<br>使用MapReduce模型解决大数据并行计算的问题，带来的最大优势，是它和Hadoop的同属一家人。因为同属于MapReduce并行编程模型，而不是MPI和OpenMP其它模型，因此，复杂的算法，只要能够以Java算法表达，在Hadoop上运行的，就能以Scala算法表达，在Spark上运行，而速度有倍数的提升。相比之下，在MPI和Hadoop算法之间切换，难度就大多了。</p>
<p><strong>（2）函数式编程</strong><br>Spark由Scala写就，而支持的语言亦是Scala。其原因之一就是Scala支持函数式编程。这一来造就了Spark的代码简洁，二来使得基于Spark开发的程序，也特别的简洁。一次完整的MapReduce，Hadoop中需要创建一个Mapper类和Reduce类，而Spark只需要创建相应的一个map函数和reduce函数即可，代码量大大降低。</p>
<p><strong>（3）Mesos</strong><br>Spark将分布式运行的需要考虑的事情，都交给了Mesos，自己不Care，这也是它代码能够精简的原因之一。</p>
<p><strong>（4）HDFS和S3</strong><br>Spark支持2种分布式存储系统：HDFS和S3。应该算是目前最主流的两种了。对文件系统的读取和写入功能是Spark自己提供的，借助Mesos分布式实现。如果自己想做集群试验，又没有HDFS环境，也没有EC2环境的话，可以搞个NFS，确保所有MESOS的Slave都可以访问，也可以模拟一下。</p>
<h2 id="Spark架构"><a href="#Spark架构" class="headerlink" title="Spark架构"></a>Spark架构</h2><p>Spark架构采用了分布式计算中的Master-Slave模型。Master是对应集群中的含有Master进程的节点，Slave是集群中含有Worker进程的节点。Master作为整个集群的控制器，负责整个集群的正常运行；Worker相当于计算节点，接收主节点命令与进行状态汇报；Executor负责任务的执行；Client作为用户的客户端负责提交应用，Driver负责控制一个应用的执行。<br><img src="http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/spark_architecture.png" alt=""></p>
<p>Spark集群部署后，需要在主节点和从节点分别启动Master进程和Worker进程，对整个集群进行控制。在一个Spark应用的执行过程中，Driver和Worker是两个重要角色。<strong>Driver 程序是应用逻辑执行的起点，负责作业的调度，即Task任务的分发，而多个Worker用来管理计算节点和创建Executor并行处理任务。在执行阶段，Driver会将Task和Task所依赖的file和jar序列化后传递给对应的Worker机器，同时Executor对相应数据分区的任务进行处理。</strong></p>
<p>Spark的整体流程为：Client 提交应用，Master找到一个Worker启动Driver，Driver向Master或者资源管理器申请资源，之后将应用转化为RDD Graph，再由DAGScheduler将RDD Graph转化为Stage的有向无环图提交给TaskScheduler，由TaskScheduler提交任务给Executor执行。在任务执行的过程中，其他组件协同工作，确保整个应用顺利执行。</p>
<pre><code>Spark架构基本组件详见该节附录。
</code></pre><h2 id="Spark运行逻辑"><a href="#Spark运行逻辑" class="headerlink" title="Spark运行逻辑"></a>Spark运行逻辑</h2><p>对于RDD，有两种类型的动作，一种是Transformation，一种是Action。它们本质区别是：</p>
<pre><code>Transformation返回值还是一个RDD。它使用了链式调用的设计模式，对一个RDD进行计算后，变换成另外一个RDD，然后这个RDD又可以进行另外一次转换。这个过程是分布式的
Action返回值不是一个RDD。它要么是一个Scala的普通集合，要么是一个值，要么是空，最终或返回到Driver程序，或把RDD写入到文件系统中
</code></pre><p><img src="http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/transformations_actions.jpg" alt=""><br>上图显示，在Spark应用中，整个执行流程在逻辑上会形成有向无环图（DAG）。Action算子触发之后，将所有累积的算子形成一个有向无环图，然后由调度器调度该图上的任务进行运算。Spark的调度方式与MapReduce有所不同。Spark根据RDD之间不同的依赖关系切分形成不同的阶段（Stage），一个阶段包含一系列函数执行流水线。图中的A、B、C、D、E、F分别代表不同的RDD，RDD内的方框代表分区。数据从HDFS输入Spark，形成RDD A和RDD C，RDD C上执行map操作，转换为RDD D， RDD B和 RDD E执行join操作，转换为F，而在B和E连接转化为F的过程中又会执行Shuffle，最后RDD F 通过函数saveAsSequenceFile输出并保存到HDFS中。</p>
<h2 id="Spark-On-Mesos"><a href="#Spark-On-Mesos" class="headerlink" title="Spark On Mesos"></a>Spark On Mesos</h2><p>为了在Mesos框架上运行，安装Mesos的规范和设计，Spark实现两个类，一个是SparkScheduler，在Spark中类名是MesosScheduler；一个是SparkExecutor，在Spark中类名是Executor。有了这两个类，Spark就可以通过Mesos进行分布式的计算。</p>
<p>Spark会将RDD和MapReduce函数，进行一次转换，变成标准的Job和一系列的Task。提交给SparkScheduler，SparkScheduler会把Task提交给Mesos Master，由Master分配给不同的Slave，最终由Slave中的Spark Executor，将分配到的Task一一执行，并且返回，组成新的RDD，或者直接写入到分布式文件系统。<br><img src="http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/spark_on_mesos.jpg" alt=""></p>
<h2 id="Spark-On-YARN"><a href="#Spark-On-YARN" class="headerlink" title="Spark On YARN"></a>Spark On YARN</h2><p>Spark on YARN能让Spark计算模型在云梯YARN集群上运行，直接读取云梯上的数据，并充分享受云梯YARN集群丰富的计算资源。</p>
<p>Spark on YARN架构解析如下：<br>基于YARN的Spark作业首先由客户端生成作业信息，提交给ResourceManager，ResourceManager在某一NodeManager汇报时把AppMaster分配给NodeManager，NodeManager启动SparkAppMaster，SparkAppMaster启动后初始化作业，然后向ResourceManager申请资源，申请到相应资源后，SparkAppMaster通过RPC让NodeManager启动相应的SparkExecutor，SparkExecutor向SparkAppMaster汇报并完成相应的任务。此外，SparkClient会通过AppMaster获取作业运行状态。<br><img src="http://7nj1qk.com1.z0.glb.clouddn.com/@/spark/intro/spark_on_yarn.jpg" alt=""></p>
<h2 id="附录"><a href="#附录" class="headerlink" title="附录"></a>附录</h2><h3 id="Spark架构中的基本组件"><a href="#Spark架构中的基本组件" class="headerlink" title="Spark架构中的基本组件"></a>Spark架构中的基本组件</h3><blockquote>
<ul>
<li>ClusterManager：在Standalone模式中即为Master（主节点），控制整个集群，监控Worker。在YARN模式中为资源管理器。 </li>
<li>Worker：从节点，负责控制计算节点，启动Executor或Driver。在YARN模式中为NodeManager，负责计算节点的控制。</li>
<li>Driver：运行Application的main()函数并创建SparkContext。</li>
<li>Executor：执行器，在worker node上执行任务的组件、用于启动线程池运行任务。每个Application拥有独立的一组Executors。</li>
<li>SparkContext：整个应用的上下文，控制应用的生命周期。</li>
<li>RDD：Spark的基本计算单元，一组RDD可形成执行的有向无环图RDD Graph。</li>
<li>DAG Scheduler：根据作业（Job）构建基于Stage的DAG，并提交Stage给TaskScheduler。</li>
<li>TaskScheduler：将任务（Task）分发给Executor执行。</li>
<li>SparkEnv：线程级别的上下文，存储运行时的重要组件的引用。</li>
<li>SparkEnv内创建并包含如下一些重要组件的引用。</li>
<li>MapOutPutTracker：负责Shuffle元信息的存储。</li>
<li>BroadcastManager：负责广播变量的控制与元信息的存储。</li>
<li>BlockManager：负责存储管理、创建和查找块。</li>
<li>MetricsSystem：监控运行时性能指标信息。</li>
<li>SparkConf：负责存储配置信息。</li>
</ul>
</blockquote>
<p><strong>转载请注明作者Jason Ding及其出处</strong><br><a href="http://jasonding1354.gitcafe.io/" target="_blank" rel="external">GitCafe博客主页(http://jasonding1354.gitcafe.io/)</a><br><a href="http://jasonding1354.github.io/" target="_blank" rel="external">Github博客主页(http://jasonding1354.github.io/)</a><br><a href="http://blog.csdn.net/jasonding1354" target="_blank" rel="external">CSDN博客(http://blog.csdn.net/jasonding1354)</a><br><a href="http://www.jianshu.com/users/2bd9b48f6ea8/latest_articles" target="_blank" rel="external">简书主页(http://www.jianshu.com/users/2bd9b48f6ea8/latest_articles)</a><br><strong>百度搜索jasonding1354进入我的博客主页</strong></p>
  
	</div>
		<footer class="article-footer clearfix">

  <div class="article-tags">
  
  <span></span> <a href="/tags/Spark/">Spark</a>
  </div>


<div class="article-categories">
  <span></span>
  <a class="article-category-link" href="/categories/Spark/">Spark</a>
</div>



<div class="article-share" id="share">

  
<div class="jiathis_style">
    <span class="jiathis_txt">分享到：</span>
    <a class="jiathis_button_tsina" title="分享到微博"><span class="jiathis_txt jiathis_separator jtico jtico_tsina">新浪微博</span></a>
    <a class="jiathis_button_weixin" title="分享到微信"><span class="jiathis_txt jiathis_separator jtico jtico_weixin">微信</span></a>
    <a class="jiathis_button_twitter" title="分享到Twitter"><span class="jiathis_txt jiathis_separator jtico jtico_twitter">Twitter</span></a>
    <a class="jiathis_button_evernote" title="分享到印象笔记"><span class="jiathis_txt jiathis_separator jtico jtico_evernote">EverNote</span></a>
    <a href="http://www.jiathis.com/share?uid=1501277" class="jiathis jiathis_txt jiathis_separator jtico jtico_jiathis" target="_blank">更多</a>
</div>
<script type="text/javascript">
    var jiathis_config={
    data_track_clickback:true,
    sm:"copy,renren,cqq",
    pic:"",
    summary:"",
    
  </script> 
<script type="text/javascript" src="//v3.jiathis.com/code/jia.js?uid=&#10;1394018007141544" charset="utf-8"></script><script type="text/javascript" src="http://v3.jiathis.com/code/plugin.client.js" charset="utf-8"></script>      


</div>
</footer>   	       
	</article>
	
<nav class="article-nav clearfix">
 
 <div class="prev">
 <a href="/2015/06/08/Machine Learning/开源图计算框架GraphLab介绍/" title="开源图计算框架GraphLab介绍">
  <strong>之后的一篇</strong><br>
  <span>
  开源图计算框架GraphLab介绍</span>
</a>
</div>


<div class="next">
<a href="/2015/06/04/Scala/【Scala】高阶函数和柯里化/" title="【Scala】高阶函数和柯里化">
 <strong>之前的一篇</strong><br> 
 <span>【Scala】高阶函数和柯里化
</span>
</a>
</div>

</nav>

	
<section class="comment">
	<div class="ds-thread" id="ds-thread"><div id="ds-waiting"></div></div>
</section>

</div>