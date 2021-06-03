---
layout: post
title: "Hadoop on Mesos"
categories: gets
tags: mesos 
---

Install
-------

### Vagrant

```
$ vagrant init precise32 http://files.vagrantup.com/precise32.box 
$ vagrant up
```

### Tools

```
$ sudo apt-get install unzip
$ sudo apt-get install curl
```

### JDK

```
$ sudo apt-get install software-properties-common
OR
$ sudo apt-get install python-software-properties
$ sudo apt-get update
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
$ java -version 
$ sudo apt-get install oracle-java8-set-default
```

---

Build HDFS
----------

```
$ wget https://github.com/mesosphere/hdfs/archive/0.1.5.tar.gz 
$ tar zxvf 0.1.5.tar.gz
```

```
$ cd hdfs-0.1.5
$ ./bin/build-hdfs
```

```
$ vagrant up
```

```
$ vagrant provision
```

### 화면

* Mesos  
http://10.141.141.10:5050
* Marathon  
http://10.141.141.10:8080 
* Chronos  
http://10.141.141.10:4400 

`/etc/hosts`
```
10.141.141.10 mesos mesos.vm
```

### VM에 SSH 접속
```
$ vagrant ssh
```

### VM 중지
```
$ vagrant halt
```

### VM 삭제
```
$ vagrant destroy
```

---

Marathon
--------

`basic.json`
```json
{
  "id": "basic",
  "cmd": "while [ true ] ; do echo 'Hello Marathon' ; sleep 5 ; done",
  "cpus": 0.1,
  "mem": 10.0,
  "instances": 1
}
```

```
$  curl -X POST -H "Content-Type: application/json" http://mesos:8080/v2/apps -d @basic.json
```

### Docker Install

```
$ vagrant ssh
$ su -
$ apt-get update
$ apt-get install docker.io
$ ln -sf /usr/bin/docker.io /usr/local/bin/docker
$ service start docker
```

`docker.json`
```json
{
  "id": "docker",
  "cmd": "python3 -m http.server 8080",
  "instances": 1,
  "cpus": 0.1,
  "mem": 32.0,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "python:3",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 8080,
          "hostPort": 0,
          "servicePort": 0
        }
      ]
    }
  },
  "healthChecks": [
    {
      "protocol": "HTTP",
      "path": "/"
    }
  ]
}
```

```
$ curl -X POST -H "Content-Type: application/json" http://mesos:8080/v2/apps -d @docker.json
```
