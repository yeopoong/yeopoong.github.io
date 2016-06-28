Docker
======

Docker 명령어 
------------

### search

>$ docker search python | less


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
  
