Ansible
=======

Ansible 설치 
------------

```
$ apt-get install ansible 
```

Ansible 설정
------------

```
$ /etc/ansible/hosts  
```

레시피 편집
----------

```
$ ansible kiss -u kyun -m setup
```

```
$ ansible kiss -u kyun -m file -a 'path=/etc/fstab' 
```