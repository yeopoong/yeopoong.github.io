---
layout: post
title: "[Spring] Simple Architecture with spring boot"
categories: dev
tags: spring spring-boot
---

Simple Architecture with spring boot
------------

  * Building simple microservices architecture using Spring Boot and React

## AWS

Spec
* t2.large, 2core, 8g

## java
```
$ sudo yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel
$ which java
$ readlink -f /usr/bin/java
```

```
cd /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64/jre/lib/security
sudo vi java.security
security.useSystemPropertiesFile=false
```

## maven

```
$ tar -xvzf apache-maven-3.6.1-bin.tar.gz
```

```
ln -s lib/apache-maven-3.6.1 maven
ln -s lib/apache-tomcat-9.0.19 tomcat
```

`.bash_profile`
```shell
PATH=$PATH:$HOME/bin

export PATH

## Maven

export M2_HOME=/home/smart/maven
export M2=$M2_HOME/bin

export PATH=$M2:$PATH

set -o vi

export CATALINA_HOME=/home/smart/tomcat
```

`.bashrc`
```shell
alias loga='tail -f ~/smart-api/logs/log-admin.out'
alias golog='cd ~/smart-api/logs'
alias gosrc='cd ~/smart-api/src'
alias gosmart='cd ~/smart-api'
```

## Git

```
$ yum install git-core
```

## Redis

```
sudo rpm -Uvh redis-6.0.5-1.el6.remi.x86_64.rpm
sudo service redis start
redis-cli
```

```
redis-cli --scan --pattern "holiday:*202007*" | xargs redis-cli unlink
redis-cli --scan --pattern "holiday:*202007*" | xargs redis-cli del

redis-cli flushall
```

## Jenkins

```
$ sudo rpm -ivh jenkins-2.235-1.1.noarch.rpm
$ sudo visudo
Defaults:jenkins !requiretty
jenkins ALL=(smart)       NOPASSWD: ALL
```

- http://127.0.0.0:8080/

- Unlock Jenkins
cat /var/lib/jenkins/secrets/initialAdminPassword

- Item
Build > Execute shell
```
sudo -iu smart sh /home/smart/shell/build-web
sudo -iu smart sh /home/smart/shell/stop-web
sudo -iu smart sh /home/smart/shell/start-web
```

```
$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
$ sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
$ sudo yum install jenkins
$ sudo vi /etc/sysconfig/jenkins
```

```
$ sudo service jenkins start
$ sudo service jenkins stop
$ sudo service jenkins restart
```

```
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Plugin

```
ren *.jpi *.hpi
```

## MySQL

backup
```
mysqldump --all-databases -uroot -p  > smart.sql
```

### mysql 8.0.19

https://dev.mysql.com/downloads/mysql/
https://dev.mysql.com/doc/refman/8.0/en/linux-installation-rpm.html

sudo yum install mysql-community-{server,client,common,libs}-*
sudo vi my.cnf
```
default-authentication-plugin=mysql_native_password
```

setenforce 0
sudo service mysqld start
sudo grep 'temporary password' /var/log/mysqld.log
```
2020-03-03T22:06:33.144755Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: .K#-y*00Mp11
```

ALTER USER 'root'@'localhost' IDENTIFIED BY 'xxxx';
SET GLOBAL validate_password.policy = 0;
SET GLOBAL sql_mode='NO_ENGINE_SUBSTITUTION';

sudo mysqld_safe --skip-grant-tables --skip-networking
mysql -u root
sudo mysqladmin shutdown

CREATE USER 'root'@'%' IDENTIFIED BY 'xxxx';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;

```
flush privileges;
UPDATE user SET authentication_string='password' WHERE user='root';
```

### TimeZone

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql
mysql -u root -p
Enter password: xxxx

mysql> SELECT @@GLOBAL.time_zone, @@SESSION.time_zone;
mysql> SET GLOBAL time_zone='UTC';
mysql> SET time_zone='UTC';
```

### mysql 5.1.74

```
$ rpm -qa | grep mysql-server
$ sudo yum install mysql-server
5.1.73-8.el6_8
$ sudo yum remove mysql
```

```
$ sudo service mysqld start
[smart@smart-dev ~]$ sudo service mysqld start
Initializing MySQL database:  WARNING: The host 'smart-dev' could not be looked up with resolveip.
This probably means that your libc libraries are not 100 % compatible
with this binary MySQL version. The MySQL daemon, mysqld, should work
normally with the exception that host name resolving will not work.
This means that you should use IP addresses instead of hostnames
when specifying MySQL privileges !
Installing MySQL system tables...
OK
Filling help tables...
OK

To start mysqld at boot time you have to copy
support-files/mysql.server to the right place for your system

PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
To do so, start the server, then issue the following commands:

/usr/bin/mysqladmin -u root password 'new-password'
/usr/bin/mysqladmin -u root -h smart-dev password 'new-password'

Alternatively you can run:
/usr/bin/mysql_secure_installation

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the manual for more instructions.

You can start the MySQL daemon with:
cd /usr ; /usr/bin/mysqld_safe &

You can test the MySQL daemon with mysql-test-run.pl
cd /usr/mysql-test ; perl mysql-test-run.pl

Please report any problems with the /usr/bin/mysqlbug script!

                                                           [  OK  ]
Starting mysqld:                                           [  OK  ]
```

```
$ /usr/bin/mysqladmin -u root password xxxx
$ mysql -uroot -p
```

Create Database & Tables
```
Username: smart
Password: smart
> create user 'smart'@'localhost' identified by 'xxxx';
> CREATE DATABASE SMARTDB CHARACTER SET UTF8;
> GRANT ALL PRIVILEGES ON SMARTDB.* TO smart@localhost;
> GRANT ALL PRIVILEGES ON SMARTDB.* TO smart@localhost IDENTIFIED BY 'xxxx';
> grant all privileges on SMARTDB.* to 'smart'@'%';
> CREATE USER 'smart'@'%' IDENTIFIED BY 'xxxx';
> GRANT ALL PRIVILEGES ON SMARTDB.* TO 'smart'@'%' WITH GRANT OPTION;
> EXIT;
$ mysql -u smart -p
> USE SMARTDB
```

```
CREATE TABLE professor ( 
    _id INT PRIMARY KEY AUTO_INCREMENT, 
    name VARCHAR(32) NOT NULL, 
    belong VARCHAR(12) DEFAULT 'FOO', 
    phone VARCHAR(12) 
) ENGINE=INNODB; 
DESCRIBE professor;
```

> mysql -u smart -h 127.0.0 -p 3306 -D SMARTDB



## Grafana

http://127.0.0.1:8080/?orgId=1

### Installing on Windows

admin/admin

Go into the conf directory and copy sample.ini to custom.ini.

`/etc/grafana/grafana.ini`
```
http_port = 3000
```

Default login and password admin/ admin / admin

Start Grafana by executing grafana-server.exe, located in the bin directory.

### Installing on RPM-based Linux

```
sudo rpm -Uvh grafana-6.2.1-1.x86_64.rpm
warning: grafana-6.2.1-1.x86_64.rpm: Header V4 RSA/SHA1 Signature, key ID 24098cb6: NOKEY
Preparing...                ########################################### [100%]
   1:grafana                ########################################### [100%]
### NOT starting grafana-server by default on bootup, please execute
 sudo /sbin/chkconfig --add grafana-server
### In order to start grafana-server, execute
 sudo service grafana-server start
POSTTRANS: Running script
```

OR

AWS install
```
### NOT starting on installation, please execute the following statements to configure grafana to start automatically using systemd
 sudo /bin/systemctl daemon-reload
 sudo /bin/systemctl enable grafana-server.service
### You can start grafana-server by executing
 sudo /bin/systemctl start grafana-server.service
POSTTRANS: Running script
```

uninstall rpm

```
rpm -qa | grep -i grafana
rpm -e grafana-5.4.2-1.x86_64
```

Enable/Disable the systemd service to start at boot

```
sudo systemctl enable grafana-server.service
sudo systemctl disable grafana-server.service
```

```
sudo service grafana-server start
sudo service grafana-server stop
sudo service grafana-server status
```

### Query

```
SELECT
  $__timeEpoch(<time_column>),
  <value column> as value,
  <series name column> as metric
FROM
  <table name>
WHERE
  $__timeFilter(time_column)
ORDER BY
  <time_column> ASC
```

## CIFS

```
yum install cifs-utils
```

`/home/smart/.smb`
```
user=smart
password=xxxx
```

* DEV
```
$ sudo mount -t cifs //127.0.0.1/img /home/smart/smart-api/img -o username=smart
$ sudo mount -t cifs -o uid=500,gid=500 //127.0.0.1/img /home/smart/smart-api/img -o username=smart
$ sudo mount -t cifs -o uid=1001,gid=1001,vers=3.0 //127.0.0.1/img /home/smart/smart-api/img -o username=smart
```

```
umount -t cifs //127.0.0.1/img
mount -t cifs
mount -a
```

`/etc/fstab`
```
//127.0.0.1/img /home/smart/smart-api/img cifs uid=500,gid=500,credentials=/home/smart/.smb,iocharset=utf8 0 0
//127.0.0.1/img /home/smart/smart-api/img cifs uid=500,gid=500,user='smart',password='xxxx',iocharset=utf8 0 0
//127.0.0.1/img /home/smart/smart-api/img cifs uid=1001,gid=1001,vers=2.1,credentials=/home/smart/.smb,iocharset=utf8 0 0
```