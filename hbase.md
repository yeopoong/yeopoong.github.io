HBase
=====

HBase table creation
---------------------

```
> list
> create 'table', 'cf'
> put 'table', 'row1', 'cf', 'value1'
> get 'table', 'row1'
> scan 'table'
```

HBase table export & import
---------------------

## Export
```
$ hbase org.apache.hadoop.hbase.mapreduce.Import "table" /home/ndap/test
```

## Import
```
$ hbase org.apache.hadoop.hbase.mapreduce.Export "table" /home/ndap/test
```
