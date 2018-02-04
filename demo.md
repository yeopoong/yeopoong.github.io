Log Monitoring Environment Setup
================================

# Hadoop

## Hadoop Architecture


## Installation & Configuration

```shell
$ sudo yum install -y java-1.8.0-openjdk-devel.x86_64
$ sudo yum list installed java*
$ sudo yum remove java*jdk
```

```
$ yum install wget
$ wget  http://mirror.navercorp.com/apache/hadoop/common/hadoop-2.7.5/hadoop-2.7.5.tar.gz
$ tar xvfz hadoop-2.7.5.tar.gz
```

```shell
$ which java
$ readlink -f /usr/bin/java
$ sudo vi /etc/profile.d/hadoop.sh
if [ "$JAVA_HOME" = "" ]
then
    export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-5.b12.el7_4.x86_64
fi

if [ "$HADOOP_OPTS" = "" ]
then
    export HADOOP_OPTS=-Djava.net.preferIPv4Stack=true
fi

if [ "$HADOOP_CONF_DIR" = "" ]
then
    export HADOOP_CONF_DIR=/home/vagrant/hadoop-2.7.5/etc/hadoop
fi

export HADOOP_HOME=/home/vagrant/hadoop
export HBASE_HOME=/home/vagrant/hbase
export ZOOKEEPER_HOME=/home/vagrant/zookeeper

PATH=$HBASE_HOME/bin:$ZOOKEEPER_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$MAVEN_HOME/bin:$JAVA_HOME/bin:$PATH:
```

```shell
$ vi /etc/hosts 
192.168.33.10 hadoop01
192.168.33.11 hadoop02
192.168.33.12 hadoop03
```

```shell
$ sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
$ sudo systemctl restart sshd
```

```shell
$ ssh-keygen -t rsa
$ ssh-add
Could not open a connection to your authentication agent.
$ eval $(ssh-agent)
$ sudo ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@hadoop01
$ sudo ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@hadoop02
$ sudo ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@hadoop03
```

```shell
$ sudo mkdir -p /home/data/hadoop/tmp
$ sudo mkdir -p /home/data/hadoop/dfs/name
$ sudo mkdir -p /home/data/hadoop/dfs/data
$ sudo chown -R vagrant:vagrant /home/data
```

`core-site.xml`
```xml
<configuration>                         
  <property>                            
    <name>fs.defaultFS</name>           
    <value>hdfs://hadoop01:9000/</value>
  </property>                           
  <property>                            
    <name>hadoop.tmp.dir</name>         
    <value>/home/data/hadoop/tmp</value>
  </property>                           
</configuration>                        
```

`hdfs-site.xml`
```xml
<configuration>                                   
  <property>                                        
    <name>dfs.replication</name>                    
    <value>3</value>                                
  </property>                                       
  <property>                                        
    <name>dfs.namenode.name.dir</name>              
    <value>file:/home/data/hadoop/dfs/name</value>  
    <final>true</final>                             
  </property>                                       
  <property>                                        
    <name>dfs.datanode.data.dir</name>              
    <value>file:/home/data/hadoop/dfs/data</value>  
    <final>true</final>                             
  </property>                                       
  <property>                            
    <name>dfs.permissions</name>        
    <value>false</value>                
  </property>                           
</configuration>                                  
```

`mapred-site.xml`
```xml
<configuration>                               
  <property>                                  
    <name>mapreduce.jobtracker.address</name> 
    <value>hadoop01:9001</value>              
  </property>                                 
  <property>                                  
    <name>mapreduce.framework.name</name>     
    <value>yarn</value>                       
  </property>                                 
</configuration>                              
```

`master`
```
hadoop01
```

`slaves`
```
hadoop01
hadoop02
hadoop03
```

```
$ scp -r hadoop-2.7.5 hadoop02:/home/vagrant
$ scp -r hadoop-2.7.5 hadoop03:/home/vagrant
```

```
$ hadoop namenode -format
$ hadoop fs -ls /
```

```
$ start-dfs.sh
$ start-yarn.sh
```

```
$ stop-dfs.sh
$ stop-yarn.sh
```

## Demo

```
$ hadoop fs -df -h
Filesystem               Size   Used  Available  Use%
hdfs://hadoop01:9000  112.4 G  200 K    106.2 G    0%

$ hadoop dfsadmin -report
```

### MapReduce Example
```
$ cd /home/vagrant/hadoop/share/hadoop/mapreduce
$ yarn jar *examples*.jar pi 50 100
```

`http://192.168.33.10:50070`

### 로컬 테스트 시 winutils.exe 오류 
> 환경변수에 HADOOP_HOME 을 설정하여 해결

1. first download winutils.exe  
: http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe 
2. create folder like c:\winutils\bin
3. copy winutils.exe insight c:\winutils\bin
4. set path HADOOP_HOME c:\winutils

# ZooKeeper

## ZooKeeper Architecture

hadoop01
hadoop02
hadoop03

## Installation & Configuration

### 설치
```
$ wget http://mirror.apache-kr.org/zookeeper/zookeeper-3.4.11/zookeeper-3.4.11.tar.gz
$ tar xfz zookeeper-3.4.11.tar.gz
$ ln -s zookeeper-3.4.11 zookeeper   
```

### ZooKeeper 설정
```
$ cd zookeeper/conf
$ cp zoo_sample.cfg zoo.cfg
$ vi zoo.cfg
dataDir=/home/data/zookeeper
server.1=hadoop01:2888:3888
server.2=hadoop02:2888:3888
server.3=hadoop03:2888:3888
```

### 
```
$ sudo mkdir /home/data/zookeeper
$ sudo chown -R vagrant:vagrant zookeeper/
$ vi /home/data/zookeeper/myid
1
```

```
$ scp -r zookeeper-3.4.11 hadoop02:/home/vagrant
$ scp -r zookeeper-3.4.11 hadoop03:/home/vagrant
```

### 시작 및 종료 
```
$ bin/zkServer.sh start
$ jps
4085 QuorumPeerMain

$ bin/zkServer.sh stop
```

## Connecting to ZooKeeper 

```
$ bin/zkCli.sh -server hadoop02
```



# HBase

## HBase Architecture

HMaster -> HRegionServer -> Region -> DataNode

HLog -> MemStore -> HFile

Compaction

## Installation & Configuration

```shell
$ wget http://apache.mirror.cdnetworks.com/hbase/1.2.6/hbase-1.2.6-bin.tar.gz
$ tar xfz hbase-1.2.6-bin.tar.gz
$ ln -s hbase-1.2.6 hbase
```

older version
```
$ wget http://archive.apache.org/dist/hbase/hbase-0.92.1/hbase-0.92.1.tar.gz
```

```shell
$ sudo mkdir -p /home/data/hbase/data
$ sodo chown -R vagrant:vagrant /home/data/hbase
```

```shell
$ vi conf/hbase-site.xml 
<configuration>
	<property>
		<name>hbase.rootdir</name>
		<value>hdfs://hadoop01:9000/hbase</value>
	</property>

	<property>
		<name>hbase.cluster.distributed</name>
		<value>true</value>
	</property>

	<property>
		<name>hbase.zookeeper.quorum</name>
		<value>hadoop01,hadoop02,hadoop03</value>
	</property>

	<property>
		<name>dfs.replication</name>
		<value>1</value>
	</property>

	<property>
		<name>hbase.zookeeper.property.clientPort</name>
		<value>2181</value> 
	</property> 

	<property>
		<name>hbase.zookeeper.property.dataDir</name>
		<value>/home/data/zookeeper</value> 
	</property> 
</configuration>
```

```shell
$ vi conf/hbase-env.sh
export HBASE_MANAGES_ZK=false
export HBASE_PID_DIR=/home/data/hbase/pids
```

```shell
$ vi conf/regionservers
hadoop01
hadoop02
hadoop03
```

```shell
$ scp -r hbase-1.2.6 hadoop02:/home/vagrant
$ scp -r hbase-1.2.6 hadoop03:/home/vagrant
```

```shell
$ bin/start-hbase.sh
$ bin/stop-hbase.sh
$ bin/hbase shell
```

Note: 프로그램에서 연결에 문제가 있을 경우 /etc/hosts 설정을 검토하자!

## UI

Master: http://192.168.33.10:16010

Region: http://192.168.33.10:16030



# Apache Phoenix

## Installation & Configuration

```
$ wget http://mirror.apache-kr.org/phoenix/apache-phoenix-4.13.1-HBase-1.2/bin/apache-phoenix-4.13.1-HBase-1.2-bin.tar.gz
$ tar xfz apache-phoenix-4.13.1-HBase-1.2-bin.tar.gz
```

```
$ cd apache-phoenix-4.13.1-HBase-1.2-bin/
$ cp phoenix-4.13.1-HBase-1.2-server.jar ../hbase/lib/
```

```
$ stop-hbase.sh
$ start-hbase.sh
```

## 사용하기

### stand-alone
```
$ cd apache-phoenix-4.13.1-HBase-1.2-bin/
$ sqlline.py localhost
sqlline version 1.2.0
0: jdbc:phoenix:localhost> !table
+------------+--------------+-------------+---------------+----------+------------+----------------------------+-------+
| TABLE_CAT  | TABLE_SCHEM  | TABLE_NAME  |  TABLE_TYPE   | REMARKS  | TYPE_NAME  | SELF_REFERENCING_COL_NAME  | REF_G |
+------------+--------------+-------------+---------------+----------+------------+----------------------------+-------+
|            | SYSTEM       | CATALOG     | SYSTEM TABLE  |          |            |                            |       |
|            | SYSTEM       | FUNCTION    | SYSTEM TABLE  |          |            |                            |       |
|            | SYSTEM       | SEQUENCE    | SYSTEM TABLE  |          |            |                            |       |
|            | SYSTEM       | STATS       | SYSTEM TABLE  |          |            |                            |       |
+------------+--------------+-------------+---------------+----------+------------+----------------------------+-------+
0: jdbc:phoenix:localhost>
```

### distributed

`sqlline.py <zookeeper_quorum>:<zookeeper_port>:<zookeeper.znode>`
```
$ sqlline.py hadoop01:2181:/hbase-unsecure
```

```sql
CREATE TABLE IF NOT EXISTS us_population (
      state CHAR(2) NOT NULL,
      city VARCHAR NOT NULL,
      population BIGINT
      CONSTRAINT my_pk PRIMARY KEY (state, city));
```

# Storm

## Architecture

## Installation & Configuration

### 설치

```
$ wget http://mirror.navercorp.com/apache/storm/apache-storm-1.1.1/apache-storm-1.1.1.tar.gz
$ tar xfz apache-storm-1.1.1.tar.gz
$ mkdir /home/data/storm
```

```
$ sudo vi /etc/profile.d/storm.sh
export STORM_HOME=/home/vagrant/storm

PATH=$STORM_HOME/bin:$PATH:
$ source /etc/profile.d/storm.sh
```

### 환경설정
```shell
$ vi conf/storm.yaml
storm.zookeeper.servers:
    - "hadoop01"
    - "hadoop02"
    - "hadoop03"

storm.local.dir: "/home/data/storm"
storm.local.hostname: "hadoop01"

nimbus.seeds: ["hadoop01"]
```

### Start nimbus(first node only)
```shell
$ nohup storm nimbus >> nimbus.log 2>&1 &
```

### Start supervisor(Each node)
```shell
$ nohup storm supervisor >> supervisor.log 2>&1 &
```

### Start storm UI(first node only)
```shell
$ nohup storm ui >> ui.log 2>&1 &
```

### Start Logviewer(Each node)
```shell
$ nohup storm logviewer > logviewer.log &
```

## Demo

http://192.168.33.10:8080

### Start Example Topology(first node only)

Build and install Storm jars locally
```
$ cd /home/vagrant/storm/examples/storm-starter
$ mvn clean install -DskipTests=true
or
$ mvn package 
```

Example 1: Run the ExclamationTopology in local mode (LocalCluster)
```
$ bin/storm jar examples/storm-starter/target/storm-starter-1.1.1.jar org.apache.storm.starter.ExclamationTopology
```

Example 2: Run the RollingTopWords in remote/cluster mode, under the name "production-topology"
```
$ bin/storm jar examples/storm-starter/target/storm-starter-1.1.1.jar org.apache.storm.starter.RollingTopWords production-topology remote
```

```
$ bin/storm list
$ bin/storm kill production-topology
```



# Spark

## Installation

```
$ curl -O http://apache.mirror.cdnetworks.com/spark/spark-2.2.1/spark-2.2.1-bin-hadoop2.7.tgz
$ tar xfz spark-2.2.1-bin-hadoop2.7.tgz
$ ln -s spark-2.2.1-bin-hadoop2.7 spark
```

```
$ sudo vi /etc/profile.d/spark.sh
export SPARK_HOME=/home/vagrant/spark
PATH=$STORM_HOME/bin:$PATH:
$ source /etc/profile
$ spark-submit --version
```

## Configuration

```shell
```

## Example

```
$ spark-submit \
--class org.apache.spark.examples.SparkPi \ 
${SPARK_HOME}/examples/jars/spark-examples_2.11-2.2.1.jar

Pi is roughly 3.143775718878594
```



# Grafana

## Installation & Configuration

```
$ sudo yum install https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.6.3-1.x86_6
4.rpm
```

## Start the server

```
$ sudo service grafana-server start
```
* This will start the grafana-server process as the grafana user, which is created during package installation.
* The default HTTP port is 3000, and default user and group is admin.

## Demo

* <http://192.168.33.20:3000>   
* login: admin/admin



# InfluxDB

## Installation

### 설치
```shell
cat <<EOF | sudo tee /etc/yum.repos.d/influxdb.repo
[influxdb]
name = InfluxDB Repository - RHEL \$releasever
baseurl = https://repos.influxdata.com/rhel/\$releasever/\$basearch/stable
enabled = 1
gpgcheck = 1
gpgkey = https://repos.influxdata.com/influxdb.key
EOF

sudo yum install influxdb
```

### 시작 및 종료
```
sudo systemctl start influxdb
sudo systemctl stop influxdb
```

## Configuration

### 설정파일
```
$ vi /etc/influxdb/influxdb.conf
```

## Demo

InfluxDB Server management
```
$ influx 
> create database garafana
> show databases
> use garafana
```



# Telegraf

## Installation
```
$ wget https://dl.influxdata.com/telegraf/releases/telegraf-1.5.1-1.x86_64.rpm
$ sudo yum localinstall telegraf-1.5.1-1.x86_64.rpm
or
$ sudo yum install -y https://dl.influxdata.com/telegraf/releases/telegraf-1.5.1-1.x86_64.rpm 
```

## Configuration
```shell
$ sudo sh -c 'telegraf -sample-config -input-filter cpu:disk:kernel:mem:net:netstat:system -output-filter influxdb > /etc/telegraf/telegraf.conf'
```

## 시작 및 종료
```
$ sudo systemctl start telegraf
$ sudo systemctl stop telegraf
```

## Demo

```shell
$ influx 
> show databases 
> use telegraf
> show measurements
> select * from cpu
```



# Kafka

## Installation & Configuration

### Kafka 설치
```
$ wget http://mirror.apache-kr.org/kafka/1.0.0/kafka_2.11-1.0.0.tgz
$ tar xfz kafka_2.11-1.0.0.tgz
$ ln -s kafka_2.11-1.0.0 kafka
```

### 시작 및 종료
```
$ bin/zookeeper-server-start.sh -daemon config/zookeeper.properties
$ bin/kafka-server-start.sh -daemon config/server.properties
$ jps
7355 QuorumPeerMain
7803 Kafka
```

## 사용하기

```
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic TopicName
Created topic "TopicName".
```

```
$ bin/kafka-topics.sh --list --zookeeper localhost:2181
TopicName
```

```
$ bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic TopicName 
```

```
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TestTopic
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic TestTopic --from-beginning
```



# Redis(Remote Dictionary Server)

## Installation & Configuration

### Installing Redis
```
$ wget http://download.redis.io/redis-stable.tar.gz
$ tar xzf redis-stable.tar.gz

$ cd redis-stable
$ sudo yum install -y gcc
$ make distclean
$ make
$ sudo make install
```

### Starting Redis

```
$ redis-server
$ redis-cli ping
PONG
```

```
$ redis-cli
CONFIG SET protected-mode no
```

redis.conf
```shell
bind 0.0.0.0
```

### Service

```
$ redis-server --service-install
$ redis-server --service-start
$ redis-server --service-stop
```

## 사용하기 

```
$ redis-cli
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> set foo bar
OK
127.0.0.1:6379> get foo
"bar"
```

# Ambari

## Installation

### Install
```
$ sudo wget -nv http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.1.2/ambari.repo -O /etc/yum.repos.d/ambari.repo

or

$ cd /etc/yum.repos.d/
$ wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.1.2/ambari.repo

$ sudo yum install ambari-server
```

### Setup
```
$ ambari-server setup
```

### Start Ambari Server
```
$ ambari-server start
```

### Deploy Cluster using Ambari Web UI
http://<ambari-server-host>:8080
admin/admin

# Java

## Installation

```
$ wget --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u162-b12/0da788060d494f5095bf8624735fa2f1/jdk-8u162-linux-x64.rpm
```
or
```
$ curl -O -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/ot
n-pub/java/jdk/8u162-b12/0da788060d494f5095bf8624735fa2f1/jdk-8u162-linux-x64.rpm
```

```
$ sudo rpm -ivh jdk-8u162-linux-x64.rpm 
or
$ sudo yum localinstall jdk-8u162-linux-x64.rpm
```

## Configuration
```
$ sudo vi /etc/profile.d/java.sh
#!/bin/bash
JAVA_HOME=/usr/java/jdk1.8.0_162/
PATH=$JAVA_HOME/bin:$PATH
export PATH JAVA_HOME
export CLASSPATH=.

$ source /etc/profile.d/java.sh
or
$ source /etc/profile

$ java -version
```



# Maven

## Installation
```
$ wget http://apache.tt.co.kr/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
$ tar xfz apache-maven-3.5.2-bin.tar.gz
$ ln -s apache-maven-3.5.2 maven
```

## Configuration
```
$ sudo vi /etc/profile.d/maven.sh
#!/bin/bash
export MAVEN_HOME=/home/vagrant/maven
export PATH=$MAVEN_HOME/bin:$PATH

$ source /etc/profile.d/maven.sh
$ mvn -version
```

### Use Exec Plugin
```
$ mvn clean compile
$ mvn exec:java -Dexec.mainClass=kyun.hadoop.HDFSClient
```

# AWS static hostname 

```
$ sudo hostnamectl set-hostname --static <persistent_host_name>
$ sudo vi /etc/cloud/cloud.cfg
preserve_hostname: true
$ sudo reboot
$ hostname
```

# Etc

```
$ unzip storm.zip -d storm
```


# Reference 

1. [Apache HBase Reference Guide][hbase]
1. [Apache Phoenix Installation](https://phoenix.apache.org/installation.html)
1. [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)
1. [Grafana Installing on RPM-based Linux](http://docs.grafana.org/installation/rpm/)
1. [Redis Quick Start][quickstart] 
1. [Ambari 설치](http://guruble.com/ambari/)


[hbase]: https://hbase.apache.org/book.html#java
[quickstart]: https://redis.io/topics/quickstart "Redis Quick Start"