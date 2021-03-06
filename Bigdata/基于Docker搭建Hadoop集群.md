
[Source](http://kiwenlau.com/2016/06/12/160612-hadoop-cluster-docker-update/ "Permalink to 基于Docker搭建Hadoop集群之升级版 | KiwenLau")

# 基于Docker搭建Hadoop集群之升级版 | KiwenLau

**摘要:** [kiwenlau/hadoop-cluster-docker][1]是去年参加[Docker巨好玩][2]比赛开发的，得了[二等奖][3]并赢了一块苹果手表，目前这个项目已经在GitHub上获得了236个Star，DockerHub的镜像下载次数2000+。总之，项目还算很受欢迎吧，这篇博客将介绍项目的升级版。

## 一. 项目介绍

将[Hadoop][4]打包到[Docker][5]镜像中，就可以快速地在单个机器上搭建Hadoop集群，这样可以方便新手测试和学习。

如下图所示，Hadoop的master和slave分别运行在不同的Docker容器中，其中hadoop-master容器中运行NameNode和ResourceManager，hadoop-slave容器中运行DataNode和NodeManager。NameNode和DataNode是Hadoop分布式文件系统HDFS的组件，负责储存输入以及输出数据，而ResourceManager和NodeManager是Hadoop集群资源管理系统YARN的组件，负责CPU和内存资源的调度。

![][6]

之前的版本使用serf/dnsmasq为Hadoop集群提供DNS服务，由于Docker网络功能更新，现在并不需要了。更新的版本中，使用以下命令为Hadoop集群创建单独的网络:



    sudo docker network create   --driver=bridge hadoop



然后在运行Hadoop容器时，使用"–net=hadoop"选项，这时所有容器将运行在hadoop网络中，它们可以通过容器名称进行通信。

**项目更新要点：**

* 去除serf/dnsmasq
* 合并Master和Slave镜像
* 使用[kiwenlau/compile-hadoop][7]项目编译的Hadoo进行安装
* 优化Hadoop配置

## 二. 3节点Hadoop集群搭建步骤

#### **1\. 下载Docker镜像**


    sudo docker pull kiwenlau/hadoop:1.0  


#### **2\. 下载GitHub仓库**

    git clone https://github.com/kiwenlau/hadoop-cluster-docker  



#### **3\. 创建Hadoop网络**



    sudo docker network create --driver=bridge hadoop   


#### **4\. 运行Docker容器**


    cd hadoop-cluster-docker  
    ./start-container.sh  


**运行结果**


    start hadoop-master container...  
    start hadoop-slave1 container...  
    start hadoop-slave2 container...  
    root@hadoop-master:~#  


* 启动了3个容器，1个master, 2个slave
* 运行后就进入了hadoop-master容器的/root目录

#### **5\. 启动hadoop**

    ./start-hadoop.sh
   
#### **6\. 运行wordcount**
    
    ./run-wordcount.sh

**运行结果**


    input file1.txt:  
    Hello Hadoop  
    input file2.txt:  
    Hello Docker  
    wordcount output:  
    Docker	1  
    Hadoop	1  
    Hello	2  



Hadoop网页管理地址:

192.168.59.1为运行容器的主机的IP。

## 三. N节点Hadoop集群搭建步骤

#### **1\. 准备**

* 参考第二部分1~3：下载Docker镜像，下载GitHub仓库，以及创建Hadoop网络

#### **2\. 重新构建Docker镜像**

#### **3\. 启动Docker容器**

* 与第2步中的N保持一致。

#### **4\. 运行Hadoop**

* 参考第二部分5~6：启动Hadoop，并运行wordcount。

## 参考

1. [基于Docker搭建多节点Hadoop集群][8]
2. [How to Install Hadoop on Ubuntu 13.10][9]

    版权声明:
    转载时请注明作者[**KiwenLau][10]**以及本文地址：
    ****

[1]: https://github.com/kiwenlau/hadoop-cluster-docker
[2]: http://www.alauda.cn/2015/04/28/docker-great/
[3]: http://www.alauda.cn/2015/06/11/presentation/
[4]: http://hadoop.apache.org/
[5]: https://www.docker.com/
[6]: http://kiwenlau.com/2016/06/12/160612-hadoop-cluster-docker-update/hadoop-cluster-docker.png
[7]: https://github.com/kiwenlau/compile-hadoop
[8]: http://kiwenlau.com/2015/06/08/150608-hadoop-cluster-docker/
[9]: https://www.digitalocean.com/community/tutorials/how-to-install-hadoop-on-ubuntu-13-10
[10]: http://kiwenlau.com "KiwenLau"
  
