Ansible
=======

Ansible 설치 
------------

```
$ apt-get install ansible 
or
$ yum install ansible 
```

Ansible 설정
------------

```
$ /etc/ansible/hosts  
```

```
$ ansible localhost -u givelink -k -m ping
SSH password: 
localhost | SUCCESS => {
    "changed": false, 
    "ping": "pong"
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

플레이북
-------

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

```
$ ansible-playbook test.yml
```

참고
---

* https://www.ansible.com/quick-start-video
* https://www.ansible.com/get-started