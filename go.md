Go
==

설치 및 환결설정
---------------

### install

```
$ wget https://storage.googleapis.com/golang/go1.6.2.linux-amd64.tar.gz  
$ sudo tar -C /usr/local -xzf go1.6.2.linux-amd64.tar.gz  
```

`.bash_profile`
```
export PATH=/usr/local/go/bin:$PATH
```

```
$ go env 
```


### GOROOT 설정

```
export GOROOT=$HOME/go 
```

tip: 설치 경로가 /usr/local/go 또는 C:\Go 라면 GOROOT를 설정할 필요가 없다

### GOPATH 설정

```
export GOPATH=$HOME/go/work 
```

```
$ sudo go get golang.org/x/tools/cmd/...
```

  
