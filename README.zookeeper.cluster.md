#集群服务启动
/data1/software/zookeeperServers/zookeeper-3.4.6_1/bin/zkServer.sh start;
/data1/software/zookeeperServers/zookeeper-3.4.6_2/bin/zkServer.sh start;
/data1/software/zookeeperServers/zookeeper-3.4.6_3/bin/zkServer.sh start;

#/data1/software/zookeeperServers/zookeeper-3.4.6_1/bin/zkCli.sh -server localhost:4180;
#/data1/software/zookeeperServers/zookeeper-3.4.6_2/bin/zkCli.sh -server localhost:4180;
#/data1/software/zookeeperServers/zookeeper-3.4.6_3/bin/zkCli.sh -server localhost:4180;

#单个服务启动
#/usr/local/zookeeper/bin/zkServer.sh start;

#zookeeper配置
#/data1/software/zookeeperServers/zookeeper-3.4.6_1/bin/../conf/zoo.cfg
#数据
#/data1/zookeeper/1/data
#日志
#/data1/zookeeper/1/logs

#查看zookeeper的状态
#echo stat | nc localhost 4180
