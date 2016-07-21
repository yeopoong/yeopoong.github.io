Docker
======

Tomcat
------

### build

`Dockerfile`
```
FROM docker.io/centos:latest
MAINTAINER  kyun <kyun@t3q.com>

RUN yum install -y java-1.8.0-openjdk net-tools wget openssh-server
RUN ssh-keygen -A
RUN echo "root:cloud3336" | chpasswd

RUN adduser tomcat
RUN echo "tomcat:cloud3336" | chpasswd

RUN su - tomcat -c "wget http://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.0.36/bin/apache-tomcat-8.0.36.tar.gz -O /home/tomcat/tomcat8.tar.gz"
RUN su - tomcat -c "tar zxvf /home/tomcat/tomcat8.tar.gz"
RUN su - tomcat -c "mv apache-tomcat-8.0.36 tomcat8"
RUN su - tomcat -c "rm -f /home/tomcat/tomcat8.tar.gz"

RUN sed -i '/\/tomcat-users/i<role rolename="manager-gui"/>' /home/tomcat/tomcat8/conf/tomcat-users.xml
RUN sed -i '/\/tomcat-users/i<role rolename="manager-script"/>' /home/tomcat/tomcat8/conf/tomcat-users.xml
RUN sed -i '/\/tomcat-users/i<user username="tomcat" password="cloud3336" roles="manager-gui, manager-script"/> ' /home/tomcat/tomcat8/conf/tomcat-users.xml

EXPOSE 22
EXPOSE 8080

CMD ["/usr/sbin/sshd","-D"]
```

>$ docker build -f tomcatDockerfile -t tomcat .


### run

>$ docker run -itd --name tomcat -p 8080:8080 tomcat

>$ docker exec tomcat su - tomcat -c "/home/tomcat/tomcat8/bin/startup.sh"


SonarQube
---------

### build

`Dockerfile`
```
FROM docker.io/centos:latest
MAINTAINER  kyun <kyun@t3q.com>

RUN yum install -y java-1.8.0-openjdk net-tools wget openssh-server unzip
RUN ssh-keygen -A
RUN echo "root:cloud3336" | chpasswd

RUN adduser sonar
RUN echo "sonar:cloud3336" | chpasswd
RUN su - sonar -c "wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.5.zip -O /home/sonar/sonarqube-5.5.zip"
RUN su - sonar -c "unzip /home/sonar/sonarqube-5.5.zip"

EXPOSE 22
EXPOSE 9000

CMD ["/usr/sbin/sshd","-D"]
```

>$ docker build -f sonarDockerfile -t sonar .


### run

>$ docker run -itd --name sonar -p 9000:9000 sonar

>$ docker exec sonar su - sonar -c "./sonarqube-5.5/bin/linux-x86-64/sonar.sh start"


Nexus
-----

### build

`Dockerfile`
```
FROM docker.io/centos:latest
MAINTAINER  kyun <kyun@t3q.com>

RUN yum install -y java-1.8.0-openjdk net-tools wget openssh-server
RUN ssh-keygen -A
RUN echo "root:cloud3336" | chpasswd

RUN adduser nexus
RUN echo "nexus:cloud3336" | chpasswd
RUN su - nexus -c "wget http://download.sonatype.com/nexus/oss/nexus-2.13.0-01-bundle.tar.gz -O /home/nexus/nexus-2.13.0-01-bundle.tar.gz"
RUN su - nexus -c "tar zxvf /home/nexus/nexus-2.13.0-01-bundle.tar.gz"
RUN su - nexus -c "mv nexus-2.13.0-01 nexus"
RUN su - nexus -c "rm -f nexus-2.13.0-01-bundle.tar.gz"

RUN sed -i '/#RUN_AS_USER=/RUN_AS_USER=nexus' /home/nexus/nexus/bin/nexus

EXPOSE 22
EXPOSE 8081

CMD ["/usr/sbin/sshd","-D"]
```

>$ docker build -f nexusDockerfile -t nexus .


### run

>$ docker run -itd --name nexus -p 8081:8081 nexus

>$ docker exec nexus su - nexus -c "./nexus/bin/nexus start"

### Nexus 서버 설정

`http://서버주소:8081/nexus` 로 접근해서 확인해 보자!

Private library repository 를 사용하기 위해서 Nexus를 설정한다.

* Nexus 서버에 접속한다.
    * [http://localhost:8081/nexus](http://localhost:8080/nexus/#welcome) 
* admin/admin123 으로 로그인한다.
* 좌측 메뉴에서 Repositories를 클릭하고 우측목록화면에서 Central Repository를 선택한다.
* Configuration 탭에서 Download Remote Indexes를 True로 변경한 후 저장한다.


Jenkins
-------

### build

`Dockerfile`  
```
FROM docker.io/centos:latest
MAINTAINER  kyun <kyun@t3q.com>

RUN yum install -y java-1.8.0-openjdk-devel net-tools wget openssh-server git maven
RUN ssh-keygen -A
RUN echo "root:cloud3336" | chpasswd

RUN adduser jenkins
RUN echo "jenkins:clou3336" | chpasswd
RUN su - jenkins -c "wget http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war -O /home/jenkins/jenkins.war"

EXPOSE 22
EXPOSE 5000

CMD ["/usr/sbin/sshd","-D"]
```

>$ docker build -f jenkinsDockerfile -t jenkins .


### run

>$ docker run -itd --name jenkins -p 5000:5000 --link tomcat:tomcat --link sonar:sonar --link nexus:nexus jenkins

>$ docker exec jenkins su - jenkins -c "java -jar jenkins.war --httpPort=5000"

note: export MAVEN_OPTS="-Xmx512m -XX:MaxPermSize=128m"

### Maven repository 설정

다음 명령으로 jenkins 컨테이너 IP 주소를 확인한다.
>$ docker inspect jenkins

SSH 로 jenkins 컨테이너에 접속한다.
>$ ssh xxx.xxx.xxx.xxx 

Nexus 서버의 접근권한을 설정하기 위해서 maven 설정파일인 `/usr/share/maven/conf/setting.xml`에 다음의 내용을 추가한다.

```
<servers>
...
    <server>
      <id>releases</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>snapshots</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>  
    <server>
      <id>thirdparty</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>
...
</servers>
```

### 플러그인 설치
 * Git plugin
 * Deploy to container Plugin

### 시스템 설정 
 * JDK 
 >`Name`: java1.8  
 >`JAVA_HOME`: /usr/lib/jvm/java-1.8.0-openjdk
 * Git 
 >`Path to Git executable`: /usr/bin/git
 * Maven
 >`Name`: maven  
 >`MAVEN_HOME`: /user/share/maven 
