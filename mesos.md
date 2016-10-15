Apache Mesos
============

Install
-------

### VirtualBox

`https://www.virtualbox.org/wiki/Downloads`

### Vagrant

`https://www.vagrantup.com/downloads.html`

---

Mesos Install
-------------

### Project 

```
$ git clone https://github.com/mesosphere/playa-mesos.git 
$ cd playa-mesos
```

```
$ bin/test 
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
