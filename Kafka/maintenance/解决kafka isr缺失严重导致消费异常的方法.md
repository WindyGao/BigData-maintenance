# 解决kafka ISR缺失严重导致消费异常的方法

## 故障现象

- 生产环境flume无法消费kafka，sink的文件为空。

- nifi中往kafka写消息报错

![img](https://img-blog.csdnimg.cn/20200619111046783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3ODY1NDIw,size_16,color_FFFFFF,t_70)

## 故障排查

- 元数据主题__consumer_offsets正常

- 对应无法消费的业务topic存在部分分区的ISR列表丢失2/3，且随着时间的推移，isr缺失的分区占比在增加

且flume端的消费组一直在rebalance。

尝试调整参数

`kafka.consumer.session.timeout.ms=30000ms`---增大消费者连接GroupCoordinator会话超时时间
![[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-50dRhE91-1592536113609)(C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20200619104612641.png)]](https://img-blog.csdnimg.cn/2020061911095486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3ODY1NDIw,size_16,color_FFFFFF,t_70)

flume sink 文件依旧为空，再次调大此参数依旧没用，flume的consumerGroup依旧显示在rebalancing



## 故障解决方法

因为之前出现过类似isr缺失的现象，当时增大了此参数

`num.replica.fetchers-------leader中进行复制的线程数，增大这个数值会增加relipca的IO`

默认是单线程，当时增加到2

但是这次的问题kafka的server.log没有任何ERROR，能看到的只有nifi生产端的无法生产的ERROR日志（连接broker失败），以及flume消费端的大批量INFO日志（consumer group is rebalancing）

抱着试一试的方式将几十台broker中的两台num.replica.fetchers参数修改为4，增大了一倍，然后重启broker

由于数据量比较庞大，且此broker正在重启，kafka server.log报错如下

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200619111121728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM3ODY1NDIw,size_16,color_FFFFFF,t_70)

属于正常状况，耐心等待重启的broker中副本加入到isr中即可

之后发现flume的sink文件大小有所增加，证明开始消费了。

最后滚动重启所有broker，flume恢复消费，nifi后续生产也不报错了。

## 疑问点

- flume修改参数，消费组日志信息中为何依旧提示持续rebalancing？

- kafka的isr缺失为何导致nifi生产端链接broker失败？---也许集群网络的问题也可能有

kafka的isr同步能力参数见链接[解决ISR丢失—— Kafka副本同步leader能力参数](https://blog.csdn.net/qq_37865420/article/details/106711362)

遇到类似isr缺失的问题可以尝试调整这些参数来解决

- 但是这些参数的调整需要与kafka的数据量作对比，现在还没有一个数据量标准来衡量这些参数设置。

  