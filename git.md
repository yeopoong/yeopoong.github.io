Git
===

Intro
-----

### 개념
  * 로컬저장소
  * 작업트리
  * 스테이징
  * 원격저장소

기본명령어 
---------

### 환경설정

>$ git config --global --list 

### 저장소 생성

>$ git init 

### Indexing 

>$ git add finaname 

### Commit 

>$ git commit -m "commit message" 


원격저장소
---------

### 원격저장소 추가

>$ git remote add origin 저장소

### Pull 

>$ git pull origin master 

### Push 

>$ git push origin master 


GitHub
------

### New SSH key

>$ ssh-keygen

```
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/kyun/.ssh/id_rsa):
/c/Users/kyun/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/kyun/.ssh/id_rsa.
Your public key has been saved in /c/Users/kyun/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:KbEV2lgElX9lozrCJQuqItEUysVPK2hhsNF+sf4ZNIQ kyun@kyun
The key's randomart image is:
+---[RSA 2048]----+
|+..  ..+=.       |
| =ooE..=..    +  |
|+o+.o+= o.   + . |
|.+o.oo++..o +    |
|.o o.oo+S+ +     |
|. . o ..+ o      |
| . . . o . .     |
|o .   o          |
|..               |
+----[SHA256]-----+
```

>$ cat ~/.ssh/id_rsa.pub 
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+gWxSuodH7OWay1HRqxG6vdoDuFsb9arRQ4RijdkdlsicisicNNJzz53II7BCNHdLs/5KEBxxdvhghjgtFMcJW1vtBXVT1LLg7HieSTfRiTdNAcR81VbtLNvxaSjhfMgacsnTY4Zc0VMMqIj7QBbDgXDQRUXVsIi8ql8yREVXdCtHngfgZqAjpyGLHPEyR3qSQqsimMpZ65WesLdwmtWbvXo6SRvu/mVc57CRqrA6riT0RfxDGpAkg8j/pkmM+Jdf+l6CPvNNIPSPdqVb9OyWatKtt+/31oFpk/yXZLOo2lkFhW+fwwc0UAy4D6tEB00Q6v2cCSefocHV0J7z5EBv kyun@kyun
```

https://github.com/settings/keys

`New SSH key`

![](image/add_ssh_key.png)


>$ ssh -T git@github.com 
```
Hi yeopoong! You've successfully authenticated, but GitHub does not provide shell access.
```

>$ git init
>$ git remote add origin git@github.com:yeopoong/basic.git

>$ git config user.name "yeopoong"
>$ git config user.email "yeopoong@gmail.com"
