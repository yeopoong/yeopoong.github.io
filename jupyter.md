Jupyter
=======

Install
-------

```
yum install -y http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm
yum install -y python-pip python-devel python-virtualenv
yum groupinstall 'Development Tools'
virtualenv jupyter-virtualenv
source jupyter-virtualenv/bin/activate
pip install jupyter
```

```
jupyter notebook --ip=192.168.33.80 --port=8080 --no-browser

jupyter notebook list
Currently running servers:
http://192.168.33.80:8080/?token=6ae364386e8bf00b9be6603a57002b2776395fc6ece07849 :: /home/vagrant
```
