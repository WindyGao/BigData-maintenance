## 故障现象
==背景==
集群规模较小，听说是本来ambari中kafka用的很正常，开发人员说flink与kafka版本不一致（具体指scala版本），然后就将HDP的kafka在ambari界面卸载了，最后安装的是apache对应版本的kafka

==问题==
更换kafka的“发行版”后，发现所有主题无法消费

## 问题排查
- 查看kafka元数据主题__consumer_offsets发现所有的副本所在brokerId格式为1001，1002格式（是HDPkafka默认的brokerId格式），所以担心之前没卸载干净
- 并且__consumer_offsets所有分区leader=-1
- describe 各个主题后发现，有些主题中的分区副本所在brokerID格式有的为1001，1002格式，有的却为1，2（估计是apache版本安装后手动设置的id）
- 查看zk节点信息，发现ids 节点的brokerId格式都是形如1，2这般
- 由此确认为元数据主题brokerId混乱,无法正常保存消费组偏移量等元数据信息
## 故障解决
- 进入zk，将元数据主题__consumer_offsets删除即可，再将同样问题的业务topic进行删除
- list查看所有主题，发现两个业务topic已经产生了（看了下参数，是允许producer自动创建的），元数据主题也自动生成了，因为一有消费者消费，他就会去创建（应该是这样，不太确定）。
- 测试生产消费，一切正常

`未曾有截图记录，还请见谅`