# HDP ports

## Atlas service ports

Note the default ports use by Apache Atlas.

The following table lists the default ports used by Apache Atlas.

| Service     | Servers           | Default Ports Used | Protocol | Description                            | Need End User Access? | Configuration Parameters |
| :---------- | :---------------- | :----------------- | :------- | :------------------------------------- | :-------------------- | :----------------------- |
| Atlas Admin | Atlas Admin Nodes | 21000              | HTTP     | Port for Atlas Admin web UI            | Yes                   | atlas.server.http.port   |
| Atlas       | Atlas Admin Nodes | 21443              | HTTPS    | Port for Atlas Admin web UI (with SSL) | Yes                   | atlas.server.https.port  |

## Flume service ports

Note the default ports used by various Flume services.

The following table lists the default ports used by the various Flume services. (**Note:** Neither of these services are used in a standard HDP installation.)

| Service | Servers                     | Default Ports Used | Protocol | Description                                                  | Need End User Access?  | Configuration Parameters                                     |
| :------ | :-------------------------- | :----------------- | :------- | :----------------------------------------------------------- | :--------------------- | :----------------------------------------------------------- |
| Flume   | Flume Agent                 | 41414              | TCP      | Flume performance metrics in JSON format                     | Yes (client API needs) | master.port.client in accumulo-site.xml                      |
| Flume   | HDFS Sink                   | 8020               | TCP      | Communication from Flume into the Hadoop cluster's NameNode  | Yes (client API needs) | tserver.port.client in accumulo-site.xml                     |
| Flume   | HDFS Sink                   | 9000               | TCP      | Communication from Flume into the Hadoop cluster's NameNode  | No                     | gc.port.client in accumulo-site.xml                          |
| Flume   | HDFS Sink                   | 50010              | TCP      | Communication from Flume into the Hadoop cluster's HDFS DataNode | No                     |                                                              |
| Flume   | HDFS Sink                   | 50020              | TCP      | Communication from Flume into the Hadoop cluster's HDFS DataNode | No                     |                                                              |
| Flume   | HDFS Sink                   | 2181               | TCP      | Communication from Flume into the Hadoop cluster's ZooKeeper | No                     |                                                              |
| Flume   | HDFS Sink                   | 16020              | TCP      | Communication from Flume into the Hadoop cluster's HBase Regionserver | No                     |                                                              |
| Flume   | All Other Sources and Sinks | Variable           | Variable | Ports and protocols used by Flume sources and sinks          | No                     | Refer to the flume configuration file(s) for ports actually in use. Ports in use are specificed using the port keyword in the Flume configuration file. By default Flume configuration files are located in /etc/flume/conf on Linux and c:\hdp\flume-1.4.0.x.y.z\conf on Windows |

## HBase service ports

Note the default ports used by various HBase services.

The following table lists the default ports used by the various HBase services.

| Service                               | Servers                                                      | Default Ports Used | Protocol | Description                                                  | Need End User Access?                     | Configuration Parameters     |
| :------------------------------------ | :----------------------------------------------------------- | :----------------- | :------- | :----------------------------------------------------------- | :---------------------------------------- | :--------------------------- |
| HMaster                               | Master Nodes (HBase Master Node and any back-up HBase Master node) | 16000              | TCP      | The port used by HBase client to connect to the HBase Master. | Yes                                       | hbase.master.port            |
| HMaster Info Web UI                   | Master Nodes (HBase master Node and back up HBase Master node if any) | 16010              | HTTP     | The port for the HBase­Master web UI. Set to -1 if you do not want the info server to run. | Yes                                       | hbase.master.info.port       |
| RegionServer                          | All Slave Nodes                                              | 16020              | TCP      | The port used by HBase client to connect to the HBase RegionServer. | Yes (Typically admins, dev/support teams) | hbase.regionserver.port      |
| RegionServer                          | All Slave Nodes                                              | 16030              | HTTP     | The port used by HBase client to connect to the HBase RegionServer. | Yes (Typically admins, dev/support teams) | hbase.regionserver.info.port |
| HBase REST Server (optional)          | All REST Servers                                             | 8080               | HTTP     | The port used by HBase Rest Servers. REST servers are optional, and not installed by default | Yes                                       | hbase.rest.port              |
| HBase REST Server Web UI (optional)   | All REST Servers                                             | 8085               | HTTP     | The port used by HBase Rest Servers web UI. REST servers are optional, and not installed by default | Yes (Typically admins, dev/support teams) | hbase.rest.info.port         |
| HBase Thrift Server (optional)        | All Thrift Servers                                           | 9090               | TCP      | The port used by HBase Thrift Servers. Thrift servers are optional, and not installed by default | Yes                                       | N/A                          |
| HBase Thrift Server Web UI (optional) | All Thrift Servers                                           | 9095               | TCP      | The port used by HBase Thrift Servers web UI. Thrift servers are optional, and not installed by default | Yes (Typically admins, dev/support teams) | hbase.thrift.info.port       |

## HDFS service ports

Note the default ports used by various HDFS services.

The following table lists the default ports used by the various HDFS services. (**Note:** Neither of these services are used in a standard HDP installation.)

| Service                              | Servers                                               | Default Ports Used                       | Protocol | Description                                                  | Need End User Access?                                        | Configuration Parameters                  |
| :----------------------------------- | :---------------------------------------------------- | :--------------------------------------- | :------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :---------------------------------------- |
| NameNode WebUI                       | Master Nodes (NameNode and any back-up NameNodes)     | 50070                                    | http     | Web UI to look at current status of HDFS, explore file system | Yes (Typically admins, Dev/Support teams, as well as extra-cluster users who require webhdfs/hftp access, for example, to use distcp) | dfs.http.address                          |
|                                      |                                                       | 50470                                    | https    | Secure http service                                          |                                                              | dfs.https.address                         |
| NameNode metadata service            |                                                       | 8020/ 9000                               | IPC      | File system metadata operations                              | Yes (All clients who directly need to interact with the HDFS) | Embedded in URI specified by fs.defaultFS |
| DataNode                             | All Slave Nodes                                       | 50075                                    | http     | DataNode WebUI to access the status, logs, etc, and file data operations when using webhdfs or hftp | Yes (Typically admins, Dev/Support teams, as well as extra-cluster users who require webhdfs/hftp access, for example, to use distcp) | dfs.datanode.http.address                 |
|                                      |                                                       | 50475                                    | https    | Secure http service                                          |                                                              | dfs.datanode.https.address                |
|                                      |                                                       | 50010SASL based IPC (non-privilege port) | IPC      | Secure data transfer                                         |                                                              | dfs.datanode.address                      |
|                                      |                                                       | 1019Privilege IPC port                   | IPC      | Secure data transfer                                         |                                                              | dfs.datanode.address                      |
|                                      |                                                       | 50020                                    | IPC      | Metadata operations                                          | No                                                           | dfs.datanode.ipc.address                  |
|                                      |                                                       | 1022                                     | https    | Customer HTTP port for Secure DataNode deployment            | Yes                                                          | dfs.datanode.http.address                 |
| Secondary NameNode                   | Secondary NameNode and any backup Secondanry NameNode | 50090                                    | http     | Checkpoint for NameNode metadata                             | No                                                           | dfs.secondary.http.address                |
| ZooKeeper Failover Controller (ZKFC) |                                                       | 8019                                     | IPC      | RPC port for Zookeeper Failover Controller                   | No                                                           | dfs.ha.zkfc.port                          |

## MapReduce service ports

Note the default port used by the various MapReduce services.

The following table lists the default ports used by the various MapReduce services.

| Service   | Servers | Default Ports Used | Protocol | Description                               | Need End User Access? | Configuration Parameters                  |
| :-------- | :------ | :----------------- | :------- | :---------------------------------------- | :-------------------- | :---------------------------------------- |
| MapReduce |         | 10020              | http     | MapReduce JobHistory server address       |                       | mapreduce.jobhistory.address              |
| MapReduce |         | 19888              | http     | MapReduce JobHistory webapp address       |                       | mapreduce.jobhistory.webapp.address       |
| MapReduce |         | 13562              | http     | MapReduce Shuffle Port                    |                       | mapreduce.shuffle.port                    |
| MapReduce |         | 19890              | https    | MapReduce JobHistory webapp HTTPS address |                       | mapreduce.jobhistory.webapp.https.address |

## YARN service ports

Note the default ports used by the various YARN services.

The following table lists the default ports used by the various YARN services.

| Service                   | Servers                                                      | Default Ports Used | Protocol | Description                          | Need End User Access?                                        | Configuration Parameters                                  |
| :------------------------ | :----------------------------------------------------------- | :----------------- | :------- | :----------------------------------- | :----------------------------------------------------------- | :-------------------------------------------------------- |
| Resource Manager WebUI    | Master Nodes (Resource Manager and any back-up Resource Manager node) | 8088               | http     | Web UI for Resource Manager          | Yes                                                          | yarn.resourcemanager.webapp.address                       |
| Resource Manager Hostname | Master Nodes (Resource Manager Node)                         | 8090               | https    | Resource Manager HTTPS Address       | Yes                                                          | yarn.resourcemanager.webapp.https.address                 |
| Resource Manager          | Master Nodes (Resource Manager Node)                         | 8050               | IPC      | For application submissions          | Yes (All clients who need to submit the YARN applications including Hive, Hive server, Pig) | Embedded in URI specified by yarn.resourcemanager.address |
| Resource Manager          | Master Nodes (Resource Manager Node)                         | 8025               | http     | For application submissions          | Yes (All clients who need to submit the YARN applications including Hive, Hive server, Pig) | yarn.resourcemanager.resource-tracker.address             |
| Scheduler                 | Master Nodes (Resource Manager Node)                         | 8030               | http     | Scheduler Address                    | Yes (Typically admins, Dev/Support teams)                    | yarn.resourcemanager.scheduler.address                    |
| Resource Manager          | Master Nodes (Resource Manager Node)                         | 8141               | http     | Scheduler Address                    | Yes (Typically admins, Dev/Support teams)                    | yarn.resourcemanager.admin.address                        |
| NodeManager               | Slave Nodes running NodeManager                              | 45454              | http     | NodeManager Address                  | Yes (Typically admins, Dev/Support teams)                    | yarn.nodemanager.address                                  |
| NodeManager               | Master Nodes (NodeManager)                                   | 8042               | http     | NodeManager Webapp Address           | Yes (Typically admins, Dev/Support teams)                    | yarn.nodemanager.webapp.address                           |
| Timeline Server           | Master Nodes                                                 | 10200              | http     | Timeline Server Address              | Yes (Typically admins, Dev/Support teams)                    | yarn.timeline-service.address                             |
| Timeline Server           | Master Nodes                                                 | 8188               | http     | Timeline Server Webapp Address       | Yes (Typically admins, Dev/Support teams)                    | yarn.timeline-service.webapp.address                      |
| Timeline Server           | Master Nodes                                                 | 8190               | https    | Timeline Server Webapp https Address | Yes (Typically admins, Dev/Support teams)                    | yarn.timeline-service.webapp.https.address                |
| Job History Service       | Master Nodes                                                 | 19888              | https    | Job History Service                  | Yes (Typically admins, Dev/Support teams)                    | yarn.log.server.url                                       |



## Hive service ports

Note the default ports used by various Hive services.

The following table lists the default ports used by the various Hive services. (**Note:** Neither of these services are used in a standard HDP installation.)

| Service        | Servers                                         | Default Ports Used | Protocol    | Description                                                  | Need End User Access?                                        | Configuration Parameters |
| :------------- | :---------------------------------------------- | :----------------- | :---------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------- |
| Hive Server    | Hive Server machine (Usually a utility machine) | 10000              | tcp or http | Service for programatically (Thrift/JDBC) connecting to Hive | Yes(Clients who need to connect to Hive either programatically or through UI SQL tools that use JDBC) | ENV Variable HIVE_PORT   |
| Hive Web UI    | Hive Server machine (Usually a utility machine) | 9999               | http        | Web UI to explore Hive schemas                               | Yes                                                          | hive.hwi.listen.port     |
| Hive Metastore |                                                 | 9083               | http        |                                                              | Yes (Clients that run Hive, Pig and potentially M/R jobs that use HCatalog) | hive.metastore.uris      |

## Kafka service ports

Note the default port used by Kafka.

The following table lists the default ports used by Kafka.

| Service | Servers      | Default Port | Default Ambari Port | Protocol | Description                | Need End User Access? | Configuration Parameters |
| :------ | :----------- | :----------- | :------------------ | :------- | :------------------------- | :-------------------- | :----------------------- |
| Kafka   | Kafka Server | 9092         | 6667                | TCP      | The port for Kafka server. |                       |                          |

## Kerberos service ports

Note the default port used by the designated Kerberos KDC.

The following table lists the default port used by the designated Kerberos KDC.

| Service | Servers             | Default Ports Used | Protocol | Description                     | Need End User Access? | Configuration Parameters |
| :------ | :------------------ | :----------------- | :------- | :------------------------------ | :-------------------- | :----------------------- |
| KDC     | Kerberos KDC server | 88                 |          | Port used by the designated KDC |                       |                          |

## Knox service ports

Note the default port used by Knox.

The following table lists the default port used by Knox.

| Service | Servers     | Default Ports Used | Protocol | Description       | Need End User Access? | Configuration Parameters |
| :------ | :---------- | :----------------- | :------- | :---------------- | :-------------------- | :----------------------- |
| Knox    | Knox server | 8443               |          | Port used by Knox |                       |                          |

## MySQL service ports

Note the default ports used by the various MySQL services.

The following table lists the default ports used by the various MySQL services.

| Service | Servers               | Default Ports Used | Protocol | Description | Need End User Access? | Configuration Parameters |
| :------ | :-------------------- | :----------------- | :------- | :---------- | :-------------------- | :----------------------- |
| MySQL   | MySQL database server | 3306               |          |             |                       |                          |

## Oozie service ports

Note the default ports used by Oozie.

The following table lists the default ports used by Oozie.

| Service | Servers      | Default Ports Used | Protocol | Description                                  | Need End User Access? | Configuration Parameters         |
| :------ | :----------- | :----------------- | :------- | :------------------------------------------- | :-------------------- | :------------------------------- |
| Oozie   | Oozie Server | 11000              | TCP      | The port Oozie server runs.                  | Yes                   | OOZIE_HTTP_PORT in oozie_env.sh  |
| Oozie   | Oozie Server | 11001              | TCP      | The admin port Oozie server runs.            | No                    | OOZIE_ADMIN_PORT in oozie_env.sh |
| Oozie   | Oozie Server | 11443              | TCP      | The port Oozie server runs when using HTTPS. | Yes                   | OOZIE_HTTPS_PORT in oozie_env.sh |

## Ranger service ports

Note the default ports used by Ranger.

The following table lists the default ports used by Ranger.

| Service             | Servers              | Default Ports Used | Protocol | Description                              | Need End User Access? | Configuration Parameters                             |
| :------------------ | :------------------- | :----------------- | :------- | :--------------------------------------- | :-------------------- | :--------------------------------------------------- |
| Ranger Admin        | Ranger Admin Nodes   | 6080               | HTTP     | Port for Ranger Admin web UI.            | Yes                   | ranger.service.http.port (in ranger-admin-site.xml)  |
| Ranger Admin        | Ranger Admin Nodes   | 6182               | HTTPS    | Port for Ranger Admin web UI (with SSL). | Yes                   | ranger.service.https.port (in ranger-admin-site.xml) |
| UNIX Auth Service   | Ranger Usersync Node | 5151               | SSL/TCP  | Port for UNIX Auth service.              | No                    | ranger.usersync.port (in ranger-ugsync-site.xml)     |
| Ranger KMS          | Ranger KMS Nodes     | 9292               | HTTP     | Port for Ranger KMS.                     | No                    | ranger.service.http.port (in kms-site.xml)           |
| Ranger KMS          | Ranger KMS Nodes     | 9293               | HTTPS    | Port for Ranger KMS.                     | No                    | ranger.service.https.port(in kms-site.xml)           |
| Solr used by Ranger | Solr                 | 6083,6183          | HTTP     | Ports for auditing to Solr.              | Yes                   | ranger-admin and all plug-ins                        |

## Sqoop service ports

Note the default ports used by Sqoop.

The following table lists the default ports used by Sqoop.

| Service | Servers       | Default Ports Used                                           | Protocol | Description                                                  | Need End User Access? | Configuration Parameters    |
| :------ | :------------ | :----------------------------------------------------------- | :------- | :----------------------------------------------------------- | :-------------------- | :-------------------------- |
| Sqoop   | Metastore     | 16000                                                        | TCP      | Connection between Sqoop and the metastore                   | No                    | sqoop.metastore.server.port |
| Sqoop   | JDBC Listener | Varies, depends on target database. For example, if moving data from MySQL, TCP port 3306 must be open. | TCP      | Outbound port from the Hadoop cluster to the database. Varies depending on Database | No                    |                             |

## Storm service ports

Note the default ports used by Storm.

The following table lists the default ports used by Storm.

| Service                | Servers | Default Port           | Default Ambari Port | Protocol | Description                                                  | Need End User Access? | Configuration Parameters |
| :--------------------- | :------ | :--------------------- | :------------------ | :------- | :----------------------------------------------------------- | :-------------------- | :----------------------- |
| ZooKeeper Port         |         | 2181                   |                     |          | Port used by localhost to talk to ZooKeeper.                 |                       | storm.zookeeper.port     |
| DRPC Port              |         | 3772                   |                     |          |                                                              |                       | drpc.port                |
| DRPC Invocations Port  |         | 3773                   |                     |          |                                                              |                       | drpc.invocations.port    |
| Nimbus Thrift Port     |         | 6627                   |                     |          |                                                              |                       | nimbus.thrift.port       |
| Supervisor Slots Ports |         | 6700, 6701, 6702, 6703 |                     |          | Defines the amount of workers that can be run on this machine. Each worker is assigned a port to use for communication. |                       | supervisor.slots.ports   |
| Logviewer Port         |         | 8000                   |                     |          |                                                              |                       | logviewer.port           |
| UI Port                |         | 8080                   | 8744                |          |                                                              |                       | ui.port                  |

## Tez ports

Note the default ports used by the various Tez services.

The following table lists the default ports used by the various Tez services.

| Service             | Servers | Default Ports Used | Protocol | Description                                        | Need End User Access?                                        | Configuration Parameters |
| :------------------ | :------ | :----------------- | :------- | :------------------------------------------------- | :----------------------------------------------------------- | :----------------------- |
| Tez AM, Tez Service |         | 12999              |          | Port to use for AMPoolService status               | Yes (Clients who need to submit Hive queries or jobs to Tez AM or Tez Service) Yes | tez.ampool.ws.port       |
|                     |         | 10030              | http     | Address on which to run the ClientRMProtocol proxy |                                                              | tez.ampool.address       |



## ZooKeeper service ports

Note the default ports used by Zookeeper service.

| Service          | Servers             | Default Ports Used | Protocol | Description                                                  | Need End User Access? | Configuration Parameters            |
| :--------------- | :------------------ | :----------------- | :------- | :----------------------------------------------------------- | :-------------------- | :---------------------------------- |
| ZooKeeper Server | All ZooKeeper Nodes | 2888               | N/A      | Port used by ZooKeeper peers to talk to each other.          | No                    | hbase.zookeeper.peerport            |
| ZooKeeper Server | All ZooKeeper Nodes | 3888               | N/A      | Port used by ZooKeeper peers to talk to each other.          | No                    | hbase.zookeeper.leaderport          |
| ZooKeeper Server | All ZooKeeper Nodes | 2181               | N/A      | Property from ZooKeeper's config zoo.cfg. The port at which the clients connect. | Yes                   | hbase.zookeeper.property.clientPort |