# [Kafka  深入解析](http://www.jasongj.com/2015/01/02/Kafka%E6%B7%B1%E5%BA%A6%E8%A7%A3%E6%9E%90/)

## key:

``` 分布式的，基于发布/订阅的消息系统， RabbitMQ，Redis, ZeroMQ, ActiveMQ, Kafka/Jafka ```

## Abstract:
```
以时间复杂度为O(1)的方式提供消息持久化能力，即使对TB级以上数据也能保证常数时间的访问性能  
高吞吐率。即使在非常廉价的商用机器上也能做到单机支持每秒100K条消息的传输  
支持Kafka Server间的消息分区，及分布式消费，同时保证每个partition内的消息顺序传输  
同时支持离线数据处理和实时数据处理  
```

## Terminology
```
1. Broker  
Kafka集群包含一个或多个服务器，这种服务器被称为broker  

2. Topic  
每条发布到Kafka集群的消息都有一个类别，这个类别被称为topic。（物理上不同topic的消息分开存储，逻辑上一个topic的消息虽然保存于一个或多个broker上但用户只需指定消息的topic即可生产或消费数据而不必关心数据存于何处）  

3. Partition  
parition是物理上的概念，每个topic包含一个或多个partition，创建topic时可指定parition数量。每个partition对应于一个文件夹，该文件夹下存储该partition的数据和索引文件   

4. Producer  
负责发布消息到Kafka broker  

5. Consumer  
消费消息。每个consumer属于一个特定的consumer group（可为每个consumer指定group name，若不指定group name则属于默认的group）。使用consumer high level API时，同一topic的一条消息只能被同一个consumer group内的一个consumer消费，但多个consumer group可同时消费这一消息。  
```
