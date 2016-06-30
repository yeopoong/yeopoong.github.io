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

RUN su - tomcat -c "wget http://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.0.35/bin/apache-tomcat-8.0.35.tar.gz -O /home/tomcat/tomcat8.tar.gz"
RUN su - tomcat -c "tar zxvf /home/tomcat/tomcat8.tar.gz"
RUN su - tomcat -c "mv apache-tomcat-8.0.35 tomcat8"
RUN su - tomcat -c "rm -f /home/tomcat/tomcat8.tar.gz"

RUN sed -i '/\/tomcat-users/i<role rolename="manager">' /home/tomcat/tomcat8/conf/tomcat-users.xml
RUN sed -i '/\/tomcat-users/i<user username="tomcat" password="cloud3336" roles="manager"/> ' /home/tomcat/tomcat8/conf/tomcat-users.xml
RUN sed -i '/\/tomcat-users/i</role>' /home/tomcat/tomcat8/conf/tomcat-users.xml

EXPOSE 22
EXPOSE 8080

CMD ["/usr/sbin/sshd","-D"]
```

>$ docker build -f tomcatDockerfile -t tomcat .


### run

>$ docker run -itd --name tomcat -p 8080:8080 tomcat

>$ docker exec tomcat su - tomcat -c "/home/tomcat/tomcat8/bin/startup.sh"

Jenkins
-------

### build

`Dockerfile`
```
FROM docker.io/centos:latest
MAINTAINER  kyun <kyun@t3q.com>

RUN yum install -y java-1.8.0-openjdk net-tools wget openssh-server
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

>$ docker run -itd --name jenkins -p 5000:5000 jenkins

>$ docker exec jenkins su - jenkins -c "java -jar jenkins.war --httpPort=5000"


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
CMD ["/home/nexus/nexus/bin/nexus start","-D"]
```

>$ docker build -f nexusDockerfile -t nexus .


### run

>$ docker run -itd --name nexus -p 8081:8081 nexus

>$ docker exec nexus su - nexus -c "./nexus/bin/nexus start"
