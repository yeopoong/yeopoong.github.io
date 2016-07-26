Hadoop
======


하둡 클러스터 노드 설정
---------------------

### EC2 인스턴스 생성

namenode
secondary-namenode
datanode1
datanode2
datanode3

### 호스트 등록
각 인스턴스의 호스트 파일에 전체 인스턴스의 호스 정보를 등록한다.

```
$ vi /etc/hosts
172.31.4.96 ip-172-31-4-96
172.31.4.92 ip-172-31-4-92
172.31.4.93 ip-172-31-4-93
172.31.4.94 ip-172-31-4-94
172.31.4.95 ip-172-31-4-95
```

### SSH 인증키 복사 

네임노드 서버의 SSH 인증키를 생성한다.
```
$ ssh-keygen -t rsa
```

생성된 인증키를 각 노드에 복사한다.
```
$ sftp ip-172-31-4-96
$ put id_rsa.pub
```

네임노드의 인증키를 로컬 SSH 인증키에 추가한다.
```
$ cat id_rsa.pub >> ~/.ssh/authorized_keys
```

---


하둡 클러스트 구성
-----------------

### 하둡 설치 

```
$ wget -L http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
$ tar xvfz hadoop-1.2.1.tar.gz 
$ ln -s hadoop-1.2.1 hadoop
```

### 하둡 환경설정 

`hadoop-env.sh`
```shell
export JAVA_HOME=/usr/lib/jvm/jre 
```

`core-site.xml`
```xml
<configuration>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://ip-172-31-4-96.ap-northeast-2.compute.internal:9000</value>
  </property>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/home/ec2-user/hadoop-data/</value>
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
    <name>dfs.http.address</name>
    <value>ip-172-31-4-96.ap-northeast-2.compute.internal:50070</value>
  </property>
  <property>
    <name>dfs.secondary.http.address</name>
    <value>ip-172-31-4-92.ap-northeast-2.compute.internal:50090</value>
  </property>
</configuration>
```

`mapred-site.xml`
```xml
<configuration>
  <property>
    <name>mapred.job.tracker</name>
    <value>ip-172-31-4-96.ap-northeast-2.compute.internal:9001</value>
  </property>
</configuration>
```

masters 파일에 보조네임노드의 호스트명을 추가한다.
`masters`
```
ip-172-31-4-92
```

slaves 파일에 데이터노드의 호스트명을 추가한다.
`slaves`
```
ip-172-31-4-93
ip-172-31-4-94
ip-172-31-4-95
```

### 하둡 배포 
네임노드의 하둡을 전체 서버에 배포한다.

```
$ cd /home/ec2-user
$ tar cfz hadoop.tar.gz hadoop-1.2.1
$ scp hadoop.tar.gz ec2-user@ip-172-31-4-92:/home/ec2-user/
```

각 노드에 접속해서 압축을 풀고 링크를 생성한다.

```
$ ssh ec2-user@ip-172-31-4-92 "cd /home/ec2-user; tar xfz hadoop.tar.gz; rm hadoop.tar.gz; ln -s hadoop-1.2.1 hadoop"
```
or
```
$ tar xfz hadoop.tar.gz
$ rm hadoop.tar.gz
$ ln -s hadoop-1.2.1 hadoop
```

### 하둡 구동 


하둡 클러스터를 실행하기 전에 다음과 같이 네임노드를 포맷한다.
```
$ ./bin/hadoop namenode -format
```

하둡 클러스터를 구동한다.
```
$ ./bin/start-all.sh
```

하둡 클러스터 노드 확인
```
$ ./bin/hadoop dfsadmin -reporth
```

---

MapReduce 
---------

### 맵리듀스 잡 실행 

샘플 데이터를 HDFS에 업로드
```
$ ./bin/hadoop fs -put conf/hadoop-env.sh conf/hadoop-env.sh
```

wordcount 예제 실행
```
$ ./bin/hadoop jar hadoop-examples-*.jar wordcount conf/hadoop-env.sh wordcount_output
```

출력 데이터 확인
```
$ ./bin/hadoop fs -cat wordcount_output/part-r-00000 | head -10
```