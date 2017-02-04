SSH
===

SSH 환경 설정하기
----------------

### SSH Diorectory

```
kyun@kiss:~/.ssh$ ll
total 16
drwx------  2 kyun kyun 4096 Feb  4 12:30 ./
drwxr-xr-x 11 kyun kyun 4096 Feb  4 12:28 ../
-rw-------  1 kyun kyun  381 Jan  6 03:53 authorized_keys
-rw-r--r--  1 kyun kyun  666 Feb  4 12:31 known_hosts
```

### SSH KEY 생성
```
kyun@kiss:~/.ssh$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/kyun/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/kyun/.ssh/id_rsa.
Your public key has been saved in /home/kyun/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:mw9eV0ACOAPcuMtGdn5pSHGHeF5jYhNODUhhXHj3kiY kyun@kiss
The key's randomart image is:
+---[RSA 2048]----+
|   ..*+B**. .    |
|    o.@oO Bo     |
|     . X.B +.    |
|    + o E + ..   |
|   + = .S+ .  .  |
|    + o +o   .   |
|   .   o+ . .    |
|       . + .     |
|        . .      |
+----[SHA256]-----+
```

생성된 파일은 다음과 같다.
```
kyun@kiss:~/.ssh$ ll
total 24
drwx------  2 kyun kyun 4096 Feb  4 13:31 ./
drwxr-xr-x 11 kyun kyun 4096 Feb  4 13:18 ../
-rw-------  1 kyun kyun  381 Jan  6 03:53 authorized_keys
-rw-------  1 kyun kyun 1675 Feb  4 13:31 id_rsa
-rw-r--r--  1 kyun kyun  391 Feb  4 13:31 id_rsa.pub
-rw-r--r--  1 kyun kyun  666 Feb  4 12:31 known_hosts
```

### 공개키 복사 
```
kyun@kiss:~/.ssh$ scp id_rsa.pub kyun@localhost:id_rsa.pub 
kyun@kiss:~/.ssh$ cat id_rsa.pub >> authorized_keys 
```