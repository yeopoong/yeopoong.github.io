Hadoop
======

HDFS
----

### HDFS 실행 

```
$ $HADOOP_HOME/bin/start-dfs.sh
$ $HADOOP_HOME/bin/start-mapred.sh
```

### HDFS 관리 페이지

```
$ http://52.78.23.190:50070/dfshealth.jsp
$ http://52.78.23.190:50030/jobtracker.jsp
```

HBase
-----

### HBase 실행
```
$ start-hbase.sh
$ hbase shell
```

### HBase 관리콘솔

```
http://192.168.33.10:60010
```

### HBase table creation

```
> list
> create 'table', 'cf'
> put 'table', 'row1', 'cf', 'value1'
> get 'table', 'row1'
> scan 'table'
```

### HBase table export & import

#### Export
```
$ hbase org.apache.hadoop.hbase.mapreduce.Import "table" /home/ndap/test
```

#### Import
```
$ hbase org.apache.hadoop.hbase.mapreduce.Export "table" /home/ndap/test
```
