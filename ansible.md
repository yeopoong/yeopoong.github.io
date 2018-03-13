Ansible
=======

Install
-------

```
$ apt-get install ansible 
or
$ yum install ansible 
```

Set up
------

```
$ /etc/ansible/hosts  
[nginx]
192.168.33.110
```

Options
* -i : (--inventory-file)
* -m : (--module-name)
* -k : (--ask-pass)

```
$ ansible localhost -u givelink -k -m ping
SSH password: 
localhost | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

```
$ ansible all -i test -m ping
```

```
$ ansible nginx -m ping
```

```
$ ansible nginx -m ping
```

Ansible Module
--------------

```
[vagrant@ansible ~]$ ansible all -m shell -a "uptime"
192.168.33.110 | SUCCESS | rc=0 >>
 06:23:43 up 49 min,  3 users,  load average: 0.00, 0.03, 0.05

[vagrant@ansible ~]$ ansible all -m shell -a "df -h"
192.168.33.110 | SUCCESS | rc=0 >>
Filesystem                       Size  Used Avail Use% Mounted on
/dev/mapper/VolGroup00-LogVol00   38G  855M   37G   3% /
devtmpfs                         236M     0  236M   0% /dev
tmpfs                            245M  132K  245M   1% /dev/shm
tmpfs                            245M  4.5M  240M   2% /run
tmpfs                            245M     0  245M   0% /sys/fs/cgroup
/dev/sda2                       1014M   63M  952M   7% /boot
tmpfs                             49M     0   49M   0% /run/user/1000
tmpfs                             49M     0   49M   0% /run/user/0

[vagrant@ansible ~]$ ansible all -m shell -a "free -h "
192.168.33.110 | SUCCESS | rc=0 >>
              total        used        free      shared  buff/cache   available
Mem:           488M        143M        7.9M        4.6M        337M        295M
Swap:          1.5G          0B        1.5G

[vagrant@ansible ~]$ ansible all -m user -a "name=ansible password=ansible" --become
192.168.33.110 | SUCCESS => {
    "changed": true,
    "comment": "",
    "createhome": true,
    "group": 1001,
    "home": "/home/********",
    "name": "VALUE_SPECIFIED_IN_NO_LOG_PARAMETER",
    "password": "NOT_LOGGING_PASSWORD",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1001
}
```

레시피 편집
----------

```
$ ansible kiss -u kyun -m setup
```

```
$ ansible kiss -u kyun -m file -a 'path=/etc/fstab' 
```

PlayBook
--------

멱등성(idempotent): 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질

```yml
---
- hosts: localhost
  user: kyun
  vars:
    warning: 'WARNING: Use by Employees ONLY'
  tasks:
    - name: setup a MOTD
      copy: dest=/home/kyun/test content={{ warning }}

  - name: wait for tomcat to start
      wait_for: port=8080 state=started
```

```yml
---
- name: Ansible test
  hosts: localhost

  tasks:
    - name: Add ansible hosts
      blockinfile:
        path: /etc/ansible/hosts
        block: |
          [test]
          192.168.33.110
```

```
$ ansible-playbook test.yml
```

```
[vagrant@ansible ~]$ sudo ansible-playbook test.yml

PLAY [Ansible test] ****************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [localhost]

TASK [Add ansible hosts] ***********************************************************************************************
changed: [localhost]

PLAY RECAP *************************************************************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```

Reference
---------

* https://www.ansible.com/quick-start-video
* https://www.ansible.com/get-started