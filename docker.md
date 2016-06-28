Docker
======

Docker 명령어 
------------

### search

>$ docker search python | less

### pull

>$ docker pull python:2.7


### start

>$ docker start [-i] [-a] <contailner>

### stop

>$ docker stop <contailner>

Dockerfile
----------

```
FROM ubuntu:14.04
MAINTAINER kyun
RUN apt-get -y install telnet
CMD ["/usr/bin/telnet", "localhost"]
```

>$ docker build -t starwars .
