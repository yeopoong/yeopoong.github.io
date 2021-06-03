---
layout: post
published: false
title: "Apache Spark Scala Tutorial For Korean"
categories: dev
tags: bigdata spark
header-img: "img/spark-logo-hd.png"
---

이 문서는 Spark 에서 Scala 언어를 사용하고자 하는 개발자를 위한 튜토리얼이다.

이 문서를 읽기 위해서는 Java 또는 Python 에 대한 지식이 있어야 하고,  Java 또는 Python 을 이용해 Spark 를 이용한 경험이 있어야 한다.

문서의 양을 줄이기 위해 Spark 에 대한 설명은 생략되며, 또한 Scala 문법중 Spark 개발에 불필요하다고 판단되는 문법 또한 생략한다.

## 참고자료

아래 주소의 내용을 참고한다.

* [HAMA 블로그](http://hamait.tistory.com/554)
* [스칼라 학교](https://twitter.github.io/scala_school/ko/index.html)
* [A free tutorial for Apache Spark.](https://github.com/deanwampler/spark-scala-tutorial)

## Scala 개발환경 구성하기

이 문서에서는 [SBT](http://www.scala-sbt.org/download.html) 를 이용해 샘플코드를 빌드하고 실행한다. 툴의 다운로드 및 설치방법은 [여기](http://www.scala-sbt.org/download.html)를 참고하기 바란다.

```sh
$ curl https://bintray.com/sbt/rpm/rpm > bintray-sbt-rpm.repo
$ sudo mv bintray-sbt-rpm.repo /etc/yum.repos.d/
$ sudo yum install sbt
$ sbt
sbt:ec2-user> exit
$
```

### Hello, World! 출력하기

아래와 같은 방법으로 간단한 테스트 프로그램을 실행시킬 수 있다.

```sh
$ mkdir sample
$ cd sample/
$ sbt console
scala> println("Hello, World!")
Hello, World!
scala> :q
$
```

## Scala Spark 프로젝트 생성하기

### 새 프로젝트 생성하기

아래 명령으로 Scala 버전을 확인한다.

```sh
$ spark-shell
......
Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_161)
......
scala> :q
```

새 프로젝트를 생성한다.

```sh
$ mkdir my_project
$ cd my_project/
$ sbt
> set name := "MyProject"
> set version := "0.1"
> set scalaVersion := "2.11.8"
> session save
> exit
```

`Main.scala` 에 아래 내용을 입력한다.

```sh
$ mkdir -p src/main/scala
$ vi src/main/scala/Main.scala
# fix linter warning
```

```scala
import org.apache.spark.SparkContext
import org.apache.spark.SparkContext._
import org.apache.spark.SparkConf

object Main {
    def main(args: Array[String]) {

        val conf = new SparkConf().setAppName("HelloWorld")
        val sc = new SparkContext(conf)

        println("===================================")
        println("Hello, world!")
        println("===================================")

        sc.stop()
    }
}
```

```sh
$ vi project/plugins.sbt
---------------------------------------------------------------------
addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.5")
---------------------------------------------------------------------

$ vi build.sbt
......
val sparkVersion = "2.3.0"
libraryDependencies ++= Seq(
  "org.apache.spark" %% "spark-core" % sparkVersion % "provided",
  "org.apache.spark" %% "spark-mllib" % sparkVersion % "provided"
)
......
```

컴파일하고 실행한다.

```sh
$ sbt assembly
$ spark-submit --class Main --master local target/scala-2.11/MyProject-assembly-0.1.jar
......
===================================
Hello, world!
===================================
......
```

## Scala Spark Example With Web Log

웹로그는 공개할 수가 없어 개인적으로 구하기 바랍니다.

Spark Shell 을 이용하는 방법과 sbt 툴을 이용하는 방법 중 sbt 툴을 이용하는 방식으로 진행한다.

아래 내용은 위에서 생성한 프로젝트 중 `Main.scala` 를 수정하는 방식으로 진행한다.

### 웹로그에서 5라인만 출력하기(with RDD)

```sh
$ vi src/main/scala/Main.scala
......
        val conf = new SparkConf().setAppName("HelloWorld")
        val sc = new SparkContext(conf)

        val log_RDD = sc.textFile("/home/ec2-user/dev/www2-www-18XXXX17.gz")
        log_RDD.take(5).map(line => println(line))

        sc.stop()
......
```

컴파일하고 실행한다.

```sh
$ sbt assembly
$ spark-submit --class Main --master local target/scala-2.11/MyProject-assembly-0.1.jar
#Software: Microsoft Internet Information Services 7.5
#Version: 1.0
#Date: 2018-04-19 08:00:00
#Fields: date time s-ip cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Referer) sc-status sc-substatus sc-win32-status time-taken
2018-04-19 08:00:00 110.93.XXX.83 GET /login/loginpage.asp vType=G 80 - 106.XXX.166.106 Mozilla/5.0+(Windows+NT+6.1;+WOW64;+Trident/7.0;+rv:11.0)+like+Gecko http://www.test.co.kr/ 302 0 0 0
```

로그파일은 로그의 첫부분에 로그파일의 포멧정보가 있다.

### 가장 많이 접속한 클라이언트 아이피 구하기(with RDD)

공백문자로 쪼갤 수 있게 되어 있다. 로그포멧은 서버설정에 의해 결정되는데 위의 경우 총 15개의 필드가 있고 9번째에 클라이언트 아이피가 있다. 이런 정보를 바탕으로 클라이언트 아이피별 조회건수를 구해보자.

```sh
$ vi src/main/scala/Main.scala
......
        val conf = new SparkConf().setAppName("HelloWorld")
        val sc = new SparkContext(conf)

        val log_RDD = sc.textFile("/home/ec2-user/dev/www2-www-18XXXX17.gz")
        val filtered_log_RDD = log_RDD.map(line => line.split(" "))
                                      .filter(line => line.size == 15)
                                      .map(arr => (arr(8), 1))
                                      .reduceByKey(_ + _)
                                      .sortBy(_._2)
        filtered_log_RDD.zipWithIndex()
                        .sortBy(_._2, ascending = false)
                        .collect
                        .foreach(row => println(row._1))

        sc.stop()
......
```

```sh
$ sbt assembly
$ spark-submit --class Main --master local target/scala-2.11/MyProject-assembly-0.1.jar
(106.XXX.166.106,1545)
(211.XXX.239.243,927)
(118.XXX.84.92,280)
(112.XXX.95.50,262)
(211.XXX.98.3,256)
(1.XXX.66.232,244)
(185.XXX.151.187,218)
(210.XXX.101.198,200)
......
```

### 이상품을 조회한 고객이 조회한 다른 상품 구하기(with RDD)

아마존에 보면 `Customers who viewed this item also viewed` 라는 서비스가 있는데 동일한 기능을 구현해 본다.

```scala
import org.apache.spark.SparkContext
import org.apache.spark.SparkContext._
import org.apache.spark.SparkConf
import org.apache.spark.mllib.rdd.RDDFunctions._

object Main {
    def main(args: Array[String]) {

        val conf = new SparkConf().setAppName("HelloWorld")
        val sc = new SparkContext(conf)

        val log_RDD = sc.textFile("/home/ec2-user/www2-www-18XXXX15.gz")
        val filtered_01_log_RDD = log_RDD.map(line => line.split(" "))
                                      .filter(line => line.size == 15)
        println("====================================================")
        println("get : log")
        println("====================================================")
        filtered_01_log_RDD.filter(row => row(4) == "/shopping/Product.asp")
                            .take(1).
                            foreach(row => println(row.mkString(" ")))

        val pattern_itemid_uid = "itemid=([0-9]+).*uid=([a-zA-Z0-9]+)".r
        val pattern_itemid = "itemid=([0-9]+)".r
        val pattern_uid = "uid=([a-z0-9]+)".r
        val filtered_02_log_RDD = filtered_01_log_RDD.filter(row => row(4) == "/shopping/Product.asp")
                                                    .map(row => (row(0), row(1), row(5)))
                                                    .map{
                                                        case (yyyymmdd, hhmmss, params) =>
                                                            val format = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
                                                            val datetime = format.parse(yyyymmdd + " " + hhmmss)
                                                            val (itemid, uid) = params match {
                                                                case pattern_itemid_uid(itemid, uid) => (itemid, uid)
                                                                case pattern_itemid(itemid) => (itemid, "")
                                                                case pattern_uid(uid) => ("", uid)
                                                                case _ => ("", "")
                                                            }
                                                            (datetime.getTime(), itemid, uid)
                                                    }
        println("====================================================")
        println("get : time / itemid / userkey")
        println("====================================================")
        filtered_02_log_RDD.take(5).foreach(row => println(row.productIterator.mkString(" ")))

        val filtered_03_log_RDD = filtered_02_log_RDD.filter(row => row._3 != "")
                                                    .sortBy(row => (row._3, row._1))
                                                    .sliding(2)
        println("====================================================")
        println("get : ((prev time / prev itemid / prev userkey), (curr time / curr itemid / curr userkey))")
        println("====================================================")
        filtered_03_log_RDD.take(5).foreach(row =>
            println("((" + row(0).productIterator.mkString(",") + "), (" + row(1).productIterator.mkString(",") + "))")
        )

        val filtered_04_log_RDD = filtered_03_log_RDD.map{
                                                        case Array(x, y) => if ((x._3 == y._3) && ((y._1 - x._1) < 8 * 60 * 1000)) {
                                                            Array(x._2, y._2)
                                                        } else { Array("", "") }
                                                    }
                                                    .filter(x => x(0) != "")
        println("====================================================")
        println("get : prev itemid / curr itemid")
        println("====================================================")
        filtered_04_log_RDD.take(5).foreach(row =>
            println(row(0) + " " + row(1))
        )

        sc.stop()
    }
}
/*
====================================================
get : log
====================================================
2018-04-27 06:00:04 110.93.XXX.83 GET /shopping/Product.asp itemid=171335 80 - 175.XXX.22.75 Mozilla/5.0+(Linux;+Android+6.0.1;+LG-F700K+Build/MMB29M)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/66.0.3359.126+Mobile+Safari/537.36 https://msearch.shopping.naver.com/ 302 0 0 15
====================================================
get : time / itemid / userkey
====================================================
1524808804000 171335
1524808805000 193274 F378BA44654B92108664BEDCAB4
1524808805000 148742 4831D53499EA3522AEEB4003212
1524808818000 126473
1524808821000 182321 B78862B4FEBA7805F5BDAB0EBD6
====================================================
get : ((prev time / prev itemid / prev userkey), (curr time / curr itemid / curr userkey))
====================================================
((1524810683000,136280,B24B0AF44FB9E25FD84BB82194E), (1524810927000,79182,D7ECC004F7385033A97194A60E8))
((1524810927000,79182,D7ECC004F7385033A97194A60E8), (1524812204000,141565,B134FC34326B4149296DC5695D8))
((1524812204000,141565,B134FC34326B4149296DC5695D8), (1524812077000,150778,5F9EF4C4921A750B782FE271D11))
((1524812077000,150778,5F9EF4C4921A750B782FE271D11), (1524810578000,129051,60C82C0484E80F61E84AA1F334F))
((1524810578000,129051,60C82C0484E80F61E84AA1F334F), (1524810678000,137584,8FD3448447EAD6D88A76AA554F8))
====================================================
get : prev itemid / curr itemid
====================================================
195509 195103
195103 195340
195340 195414
195414 195078
195078 195899
*/
```

웹 URL 에 userKey 를 넣어두었다면 그걸 이용하면 되고, 없다면 clientip 를 이용해도 꽤 유사한 결과를 얻을 수 있다.

`sliding()` 을 이용하면 이전 로그라인과 현재 로그라인을 한줄로 만들 수 있다. 그중에 userKey 가 동일하고, 상품페이지 조회시간 간격이 8분 미만인 내역만 뽑으면 위와 같이 이전에 조회한 상품코드와 현재 조회하고 있는 상품코드를 구할 수 있다.

여기서 다시 이전 상품코드로 `groupBy()` 하면 특정 상품을 조회한 고객이 다음에 조회한 상품, 즉 `Customers who viewed this item also viewed` 를 구할 수 있다.

### 이상품을 조회한 고객이 조회한 다른 상품 구하기(with Dataset)

위 소스를 Dataset 을 이용해 다시 구현해 보자. `Dataset` 은 `RDD` 에 비해 2배 속도가 빠르고, 메모리 소모량이 1/4 이라고 하니 어쩔 수 없는 상황이 아니면 `Dataset` 을 쓰도록 하자.

```sh
$ vi build.sbt
......
val sparkVersion = "2.3.0"
libraryDependencies ++= Seq(
  "org.apache.spark" %% "spark-core" % sparkVersion % "provided"
  , "org.apache.spark" %% "spark-sql" % sparkVersion % "provided"
  // , "org.apache.spark" %% "spark-mllib" % sparkVersion % "provided"
  , "org.apache.hadoop" % "hadoop-aws" % "2.7.6" % "provided"
)
......
```

```scala
// -*- coding: utf-8 -*-
import org.apache.spark.SparkContext
import org.apache.spark.SparkContext._
import org.apache.spark.SparkConf
import org.apache.spark.sql._

object Main {
    case class RawLog(yyyymmdd: String, hhmmss: String, params: String)
    case class FilteredLog(unixtime: Long, itemid: String, uid: String)

    def main(args: Array[String]) {

        val conf = new SparkConf().setAppName("DS Project")
        val sc = new SparkContext(conf)
        val spark = SparkSession.builder()
                        .appName("DS Project")
                        .getOrCreate()

        val sqlContext= new SQLContext(sc)
        import sqlContext.implicits._

        // spark-shell 에서 테스트하려면 아래 내용을 입력해 주어야 한다.
        // $ vi spark/conf/spark-defaults.conf
        // spark.jars.packages    org.apache.hadoop:hadoop-aws:2.7.6

        // ==========================================================
        // S3 접속을 위한 설정하기
        val region = "ap-northeast-2"
        System.setProperty("com.amazonaws.services.s3.enableV4", "true")
        sc.hadoopConfiguration.set("fs.s3a.impl", "org.apache.hadoop.fs.s3a.S3AFileSystem")
        sc.hadoopConfiguration.set("com.amazonaws.services.s3.enableV4", "true")
        sc.hadoopConfiguration.set("fs.s3a.endpoint", "s3." + region + ".amazonaws.com")

        // ==========================================================
        // RDD 포멧으로 로그파일 열기
        val rdd = sc.textFile("s3a://버킷이름/파일이름")
                    .map(line => line.split(" "))
                    .filter(line => line.size == 15 && line(4) == "/shopping/Product.asp")
                    .map(row => RawLog(row(0), row(1), row(5)))

        // ==========================================================
        // DataFrame 으로 변경
        val df = rdd.toDF()
        // df.show()

        val pattern_itemid_uid = "itemid=([0-9]+).*uid=([a-zA-Z0-9]+)".r
        val pattern_itemid = ".*itemid=([0-9]+).*".r
        val pattern_uid = ".*uid=([a-z0-9]+).*".r
        val format = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")

        // ==========================================================
        // Dataset 으로 변경
        val ds = df.map(row => {
            val yyyymmdd = row.getAs[String]("yyyymmdd")
            val hhmmss = row.getAs[String]("hhmmss")
            val params = row.getAs[String]("params")

            val datetime = format.parse(yyyymmdd + " " + hhmmss)
            val (itemid, uid) = params match {
                case pattern_itemid_uid(itemid, uid) => (itemid, uid)
                case pattern_itemid(itemid) => (itemid, "")
                case pattern_uid(uid) => ("", uid)
                case _ => ("", "")
            }

            val unixtime = datetime.getTime() / 1000
            FilteredLog(unixtime, itemid, uid)
        })
        .filter(row => row.uid != "")
        //ds.show()

        ds.createOrReplaceTempView("tv_row_log")

        val resultDS = spark.sql("""
            SELECT T.prev_itemid, T.itemid, COUNT(*) as cnt
            FROM
                (
                    SELECT
                        unixtime, itemid
                        , lag(itemid) OVER (PARTITION BY uid ORDER BY unixtime) AS prev_itemid
                        , lag(unixtime) OVER (PARTITION BY uid ORDER BY unixtime) AS prev_unixtime
                    FROM tv_row_log
                ) T
            WHERE
                1 = 1
                AND T.prev_itemid is not NULL
                AND (unixtime - prev_unixtime) <= 8 * 60
                AND itemid <> prev_itemid
            GROUP BY
                T.prev_itemid, T.itemid
            ORDER BY
                cnt desc, T.prev_itemid, T.itemid
        """)
        resultDS.show()

        sc.stop()
    }
}
```

기존에 `sliding` 함수에 비해 `lag` 이 더 깔끔하게 동작한다.