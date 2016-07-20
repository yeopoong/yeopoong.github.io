Docker
======

Docker Install 
--------------

### install

>$ sudo yum install docker

### start

>$ sudo service docker start

루트가 아닌 계정에 권한 부여하기
------------------------------

>$ sudo groupadd docker  
>$ sudo gpasswd -a $(whoami) docker  
>$ sudo service docker restart

note: You will need to logout and log back in, in order to have the group update take effect.

Docker 명령어 
------------

### search

>$ docker search python | less

### pull

>$ docker pull python:2.7

### run

>$ docker run -i -t -d ubuntu echo Hello World!

* -d, --detach : 컨테이너를 백그라운드에서 실행
* -i, --interactive : 컨테이너가 실행된 이후에도 컨테이너와 연결된 표준 입력을 유지
* -t, --tty : 가상 터미널을 활성화하며 컨테이너의 터미널로 직접 연결할 때 사용 


### start

>$ docker start [-i] [-a] <container>

### stop

>$ docker stop <container>

### exec

>$ docker exec -it <container> bash

### rm
docker rm $(docker ps -a -q)


Build
-----

`Dockerfile`
```
FROM ubuntu:14.04
MAINTAINER kyun
RUN apt-get -y install telnet
CMD ["/usr/bin/telnet", "localhost"]
```

>$ docker build -t starwars .


Docker Compose
--------------

### Install

>$ curl -L https://github.com/docker/compose/releases/download/1.6.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

  
>$ chmod +x /usr/local/bin/docker-compose


`docker-compose.yml`
```
version: '2'
services:
  tomcat:
    build: tomcatDockerfile
    ports:
     - "8080:8080"
  nexus:
    build: nexusDockerfile
    ports:
     - "8081:8081"
  sonar:
    build: sonarDockerfile
    ports:
     - "9000:9000"
  jenkins:
    build: jenkinsDockerfile
    ports:
     - "5000:5000"
    links:
     - tomcat
     - nexus
     - sonar
```

