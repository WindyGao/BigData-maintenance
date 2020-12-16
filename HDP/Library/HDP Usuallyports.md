# HDP ports



## HDFS service ports

| Service                              | Servers                                               | Default Ports Used | Protocol | Description                                                  | Need End User Access?                                        | Configuration Parameters                  |
| :----------------------------------- | :---------------------------------------------------- | :----------------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :---------------------------------------- |
| NameNode WebUI                       | Master Nodes (NameNode and any back-up NameNodes)     | 50070              | http     | Web UI to look at current status of HDFS, explore file system | Yes (Typically admins, Dev/Support teams, as well as extra-cluster users who require webhdfs/hftp access, for example, to use distcp) | dfs.http.address                          |
| NameNode metadata service            |                                                       | 8020/ 9000         | IPC      | File system metadata operations                              | Yes (All clients who directly need to interact with the HDFS) | Embedded in URI specified by fs.defaultFS |
| Secondary NameNode                   | Secondary NameNode and any backup Secondanry NameNode | 50090              | http     | Checkpoint for NameNode metadata                             | No                                                           | dfs.secondary.http.address                |
| ZooKeeper Failover Controller (ZKFC) |                                                       | 8019               | IPC      | RPC port for Zookeeper Failover Controller                   | No                                                           | dfs.ha.zkfc.port                          |

## Hive service ports

| Service                | Servers                                                      | Default Ports Used | Protocol    | Description                                                  | Need End User Access?                                        |
| :--------------------- | :----------------------------------------------------------- | :----------------- | :---------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Hive Server            | Hive Server machine (Usually a utility machine)              | 10000              | tcp or http | Service for programatically (Thrift/JDBC) connecting to Hive | Yes(Clients who need to connect to Hive either programatically or through UI SQL tools that use JDBC) |
| Hive Metastore         |                                                              | 9083               | http        |                                                              | Yes (Clients that run Hive, Pig and potentially M/R jobs that use HCatalog) |
| MapReduce              |                                                              | 19888              | http        | MapReduce JobHistory webapp address                          |                                                              |
| Resource Manager WebUI | Master Nodes (Resource Manager and any back-up Resource Manager node) | 8088               | http        | Web UI for Resource Manager                                  | Yes                                                          |
| NodeManager            | Master Nodes (NodeManager)                                   | 8042               | http        | NodeManager Webapp Address                                   | Yes (Typically admins, Dev/Support teams)                    |
| Timeline Server        | Master Nodes                                                 | 10200              | http        | Timeline Server Address                                      | Yes (Typically admins, Dev/Support teams)                    |
| Timeline Server        | Master Nodes                                                 | 8188               | http        | Timeline Server Webapp Address                               | Yes (Typically admins, Dev/Support teams)                    |
| Job History Service    | Master Nodes                                                 | 19888              | https       | Job History Service                                          | Yes (Typically admins, Dev/Support teams)                    |

## Kafka service ports

Note the default port used by Kafka.

| Service        | Servers      | Default Port | Default Ambari Port | Protocol | Description                |
| :------------- | :----------- | :----------- | :------------------ | :------- | :------------------------- |
| Kafka          | Kafka Server | 9092         | 6667                | TCP      | The port for Kafka server. |
| ZooKeeper Port |              | 2181         | 2181                |          |                            |

## Spark service ports

| Service               | Servers | Default Port | Default Ambari Port | Protocol | Description | Need End User Access? | Configuration Parameters |
| :-------------------- | :------ | :----------- | :------------------ | :------- | :---------- | :-------------------- | :----------------------- |
| spark.history.ui.port |         | 18081        |                     |          |             |                       |                          |
| Livy for spark server |         | 8999         |                     |          |             |                       |                          |
| spark2 thrift server  |         | 10016        |                     |          |             |                       |                          |

## Phoenix  service ports

| Service             | Servers                                                      | Default Ports Used | Protocol | Description                                                  | Need End User Access?                     |
| :------------------ | :----------------------------------------------------------- | :----------------- | :------- | :----------------------------------------------------------- | :---------------------------------------- |
| HMaster             | Master Nodes (HBase Master Node and any back-up HBase Master node) | 16000              | TCP      | The port used by HBase client to connect to the HBase Master. | Yes                                       |
| HMaster Info Web UI | Master Nodes (HBase master Node and back up HBase Master node if any) | 16010              | HTTP     | The port for the HBase­Master web UI. Set to -1 if you do not want the info server to run. | Yes                                       |
| RegionServer        | All Slave Nodes                                              | 16020              | TCP      | The port used by HBase client to connect to the HBase RegionServer. | Yes (Typically admins, dev/support teams) |
| RegionServer        | All Slave Nodes                                              | 16030              | HTTP     | The port used by HBase client to connect to the HBase RegionServer. | Yes (Typically admins, dev/support teams) |
| ZooKeeper Port      |                                                              | 2181               |          |                                                              |                                           |