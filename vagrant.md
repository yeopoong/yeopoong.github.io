Vagrant
=======

Vagrant Install 
---------------

### install

https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5.msi

---

Vagrant Command 
---------------

### init

#### Ubuntu
```
$ vagrant init precise64 http://files.vagrantup.com/precise64.box 
```
OR
```
$ vagrant box add precise64 http://files.vagrantup.com/precise64.box 
$ vagrant init precise64
```

#### Centos

```
$ vagrant box add centos/7
```

`Vagrantfile`
```
  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "private_network", ip: "192.168.33.10"
```

브리지 모드로 시작하기  
`Vagrantfile`
```
  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"
  config.vm.network "public_network", bridge: "eth0"
```

### up

```
$ vagrant up
```

### ssh 

```
$ vagrant ssh 
Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
New release '14.04.5 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Welcome to your Vagrant-built virtual machine.
Last login: Sat Sep  3 23:00:55 2016 from 10.0.2.2
```

note: there's no /etc/os-release file in Ubuntu 12.04, which Vagrant 1.8.5 rely on to detect Ubuntu.

```
$ cat /etc/os-release
NAME="Ubuntu"
VERSION="12.04 LTS, Precise Pangolin"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu precise (12.04 LTS)"
VERSION_ID="12.04"
```

### list 

```
$ vagrant box list 
```

### halt 

```
$ vagrant halt
```

---

JDK Install 
-----------

```
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```

note: 
$ sudo apt-get install software-properties-common


