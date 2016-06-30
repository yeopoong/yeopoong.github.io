개발환경
=======

Jenkins 
-------

http://jenkins-ci.org/

```
# adduser jenkins
# su - jenkins
# wget http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war
# java -jar jenkins.war --httpPort=5000
```

`http://호스트:5000/`로 접근해서 확인해 보자! 

### 플러그인 설치
 * Git plugin
 * Deploy to container Plugin
 * SonarQube Plugin

### 시스템 설정 
 * SonarQube servers 
 >`Name`: SonarQube5.5  
 >`Server URL`: http://192.168.0.52:9000/
 * JDK 
 >`Name`: java1.8  
 >`JAVA_HOME`: /usr/lib/jvm/jre-1.8.0
 * Git 
 >`Path to Git executable`: /usr/bin/git
 * Maven
 >`Name`: maven  
 >`MAVEN_HOME`: /user/share/maven 


SonarQube
---------

```
# adduser sonar
# su - sonar
# wget https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-5.5.zip
# unzip sonarqube-5.5.zip
# ./sonarqube-5.5/bin/linux-x86-64/sonar.sh start
```

`http://서버주소:9000/` 로 접근해서 확인해 보자! (admin/admin)


Nexus
-----

```
# adduser nexus
# su - nexus
# wget  http://download.sonatype.com/nexus/oss/nexus-2.13.0-01-bundle.tar.gz
# tar zxvf nexus-2.13.0-01-bundle.tar.gz
# ln -s nexus-2.13.0-01 nexus
# vi nexus/bin/nexus
  RUN_AS_USER=nexus
# ./nexus/bin/nexus start
```

`http://서버주소:8081/nexus` 로 접근해서 확인해 보자!
  
