---
layout: post
title: "HBase to Hive"
subtitle: "HBase to Hive"
categories: dev
tags: data
---

HBase to Hive
=============

HBase Table Creation
---------------------

```
# /usr/local/hbase/bin/hbase shell
hbase> create 'short_urls', {NAME=>'u'},{NAME=>'s'}
hbase> put 'short_urls', 'bit.ly/aaaa', 's:hits', '100'
hbase> put 'short_urls', 'bit.ly/aaaa', 'u:url', 'hbase.apache.org'
hbase> put 'short_urls', 'bit.ly/abcd', 's:hits', '123'
hbase> put 'short_urls', 'bit.ly/abcd', 'u:url', 'example.com/foo'
hbase> scan 'short_urls'
```

Hive Table Creation
-------------------

```
# /usr/local/hive/bin/hive
hive> CREATE EXTERNAL TABLE short_urls(short_url string, url string, hit_count int) STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' WITH SERDEPROPERTIES("hbase.columns.mapping" = ":key,u:url,s:hits") TBLPROPERTIES("hbase.table.name"="short_urls");
```

Hive Environment 
----------------

```
$ vi /usr/local/hive/conf/hive-site.xml
<property>
    <name>hive.aux.jars.path</name>
    <value>file:///usr/local/hive/lib/guava-r09.jar,file:///usr/local/hive/lib/hbase-0.92.0.jar,file:///usr/local/hive/lib/hive-hbase-handler-0.9.0.jar,file:///usr/local/hive/lib/zookeeper-3.4.3.jar</value>
</property>
```
