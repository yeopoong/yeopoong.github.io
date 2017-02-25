HBase Backup 
============
> 전체 클러스터를 종료하는 방법과 클러스터에서 백업하는 방법이 있음.

1.Full Shutdown Backup
--------------------
* 가장 쉽고 빠른 방법이지만 증분 백업이 불가능 하고, 
* HBase 클러스터를 종료 할 수 있는 경우만 사용할 수 있다.
* 변경 사항을 누락 시킬 가능성이 없다.

2.Live Cluster Bacup
--------------------

## 2.1 Replication
* 두 번째 클러스터가 있을 경우에 가능한다.
* 클러스터 간 로그 전송에 의해서 비동기적으로 행해진다. 

## 2.2 CopyTable

* 테이블 복사 맵리듀스 잡을 통한 백업이다.
* 덤프 파일을 생성하지 않으며 직접 타깃 테이블에 행해진다.
* 같은 클러스트 또는 다른 클러스터 모두 가능하다.
* 증분백업이 가능하다.
* 클러스터가 가동 중이기 때문에 복사 프로세스에서 편집 내용을 놓칠 수 있는 위험이 있다.

## 2.3 Export

* 동일한 클러스터의 HDFS 에 테이블의 내용을 덤프한다.
* 맵리듀스 잡을 통한 백업이다.
* 증분백업이 가능하다.
* 클러스터가 가동 중이기 때문에 복사 프로세스에서 편집 내용을 놓칠 수 있는 위험이 있다.

### Export
dump the contents of table to HDFS
```
$ hbase org.apache.hadoop.hbase.mapreduce.Export <tablename> <outputdir> <versions> <starttime> <endtime>
```

### Import
load data that has been exported back into HBase.
```
$ hbase org.apache.hadoop.hbase.mapreduce.Import <tablename> <inputdir>
```

