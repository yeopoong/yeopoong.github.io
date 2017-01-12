개발서버 설정
============

JAVA
----

JAVA8 설치
```
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```

설치확인
```
$ java -version 
$ javac -version 
```

TOMCAT
------

Tomcat 8 Downloads
```
$ wget http://apache.tt.co.kr/tomcat/tomcat-8/v8.5.9/bin/apache-tomcat-8.5.9.tar.gz 
```

Tomcat Setup 
```
$ tar xfz apache-tomcat-8.5.9.tar.gz
$ ln -s apache-tomcat-8.5.9/ tomcat
```


MAVEN
-----

Maven Downloads
```
$ wget http://mirror.navercorp.com/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
```

Maven Setup 
```
$ tar xfz apache-maven-3.3.9-bin.tar.gz
$ ln -s apache-maven-3.3.9/ maven
```

환경설정
-------

/etc/profile
```sh
# Tomcat Env
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export CATALINA_HOME=/home/kyun/tomcat
export CLASSPATH=.:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar:$CATALINA_HOME/lib/jsp-api.jar:$CATALINA_HOME/lib/servlet-api.jar
export M2_HOME=/home/kyun/maven
PATH=$PATH:$JAVA_HOME/bin:$M2_HOME/bin:$CATALINA_HOME/bin
```

방화벽 해제
```
$ sudo ufw allow 8080/tcp
```