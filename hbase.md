HBase
=====

HBase Intall 
------------

### HBase download
```
$ mkdir hbase-install
$ cd hbase-install
$ wget http://apache.tt.co.kr/hbase/0.98.24/hbase-0.98.24-hadoop1-bin.tar.gz
$ tar xvfz hbase-0.98.24-hadoop1-bin.tar.gz
$ ln -s ./hbase-install/hbase-0.98.24-hadoop1 hbase
```

### HBASE_HOME 설정
```
$ export HBASE_HOME=`pwd`/hbase
$ export PATH=$PATH:$HBASE_HOME/bin
```

### JAVA_HOME 설정
```
$ which java
$ readlink -f /usr/bin/java
$ export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

### HBase 설정

`/etc/hbase/conf/`
```
$ hbase-env.sh 
$ hbase-site.xml 
```

### HBase 관리콘솔

```
http://192.168.33.10:60010
```

### HBase 실행
```
$ start-hbase.sh
$ hbase shell
```


HBase table creation
---------------------

```
> create 'table', 'cf'
> list
> describe 'table'
> put 'table', 'row1', 'cf', 'value1'
> get 'table', 'row1'
> scan 'table'
```

HBase table export & import
---------------------------

### Export
```
$ hbase org.apache.hadoop.hbase.mapreduce.Import "table" /home/ndap/test
```

### Import
```
$ hbase org.apache.hadoop.hbase.mapreduce.Export "table" /home/ndap/test
```
