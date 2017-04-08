Hadoop
======


프로토콜 버터 설치
-----------------

```
$ wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
$ tar xvfz protobuf-2.5.0.tar.gz
$ mv protobuf-2.5.0 /usr/local/src
$ ./configure
$ make
$ make install
```

* 만약, GCC 설치가 않되어 있을 경우 설치한다.
```
$ yum install gcc
$ yum install gcc-c++
$ yum install glibc-devel
```

하둡2 설치 
---------

```
$ wget http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-2.6.5/hadoop-2.6.5.tar.gz
$ tar xvfz hadoop-2.6.5.tar.gz
$ mv hadoop-2.6.5 /home/hadoop
$ ln -s hadoop-2.6.5/ hadoop
$ ssh-keygen -t rsa
$ cat id_rsa.pub >> authorized_key
$ chmod 644 authorized_key
```

하둡 환경설정 
-----------

`/etc/profile`
```shell
export JAVA_HOME=/usr/lib/jvm/jre 
```

`hadoop/etc/hadoop/masters`
```
hostname
```

`hadoop/etc/hadoop/slaves`
```
hostname
```

`core-site.xml`
```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://ip-172-31-1-254:9010</value>
  </property>
</configuration>
```

`hdfs-site.xml`
```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>

  <property>
    <name>dfs.namenode.name.dir</name>
    <value>/home/hadoop/data/dfs/namenode</value>
  </property>

  <property>
    <name>dfs.namenode.checkpoint.dir</name>
    <value>/home/hadoop/data/dfs/namesecondary</value>
  </property>

  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/home/hadoop/data/dfs/datanode</value>
  </property>

  <property>
    <name>dfs.http.address</name>
    <value>ip-172-31-1-254:50070</value>
  </property>

  <property>
    <name>dfs.secondary.http.address</name>
    <value>ip-172-31-1-254:50090</value>
  </property>

</configuration>
```

`mapred-site.xml`
```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>
```

`yarn-site.xml`
```xml
<configuration>

<!-- Site specific YARN configuration properties -->
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>

  <property>
    <name>yarn.nodemanager.aux-services.mapreduce_shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>

  <property>
    <name>yarn.nodemanager.local-dirs</name>
    <value>/home/hadoop/data/yarn/nm-local-dir</value>
  </property>

  <property>
    <name>yarn.resourcemanager.fs.state-store.uri</name>
    <value>/home/hadoop/data/yarn/system/rmstore</value>
  </property>

  <property>
    <name>yarn.resourcemanager.hostname</name>
    <value>ip-172-31-1-254</value>
  </property>

</configuration>
```

### 하둡 구동 

하둡 클러스터를 실행하기 전에 다음과 같이 네임노드를 포맷한다.
```
$ ./bin/hdfs namenode -format
```

하둡 클러스터를 구동한다.
```
$ ./bin/start-all.sh
$ ./sbin/mr-jobhistory-daemon.sh start historyserver
```