---
layout: post
title: "Running Local Jupyter Env with docker"
categories: dev
tags: infra docker
---

> Create local Jupyter or JupyterLab dev environment using Docker

## Steps: 

1. First we need to create a docker hub account (free). Just load https://hub.docker.com/ and register.

2. Download docker from docker store and install it on your machine.

3. Once you have finished installation, login using your docker hub credentials. 

4. Open a terminal and execute a command to download and run jupyter/all-spark-notbook docker image (it will take some time to download docker images).

## Jupyter:  

```
$ docker run -it --rm -p 8888:8888 -p 4040:4040 -v ~:/home/jovyan/work jupyter/all-spark-notebook
```

## JupyterLab:  

```
$ docker run --rm -p 8888:8888 -p 4040:4040 -e JUPYTER_ENABLE_LAB=yes -v ~:/home/jovyan/work jupyter/all-spark-notebook
```

## Connect the Jupyter Notebook

Copy/paste this URL into your browser when you connect for the first time, to login with a token:
  http://(dc8f177e2ddf or 127.0.0.1):8888/?token=612c3600c0a296bee08471935dd321fe727f1d61afd3a517

## Test

create a simple Spark DataFrame
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local").appName("Hello World").getOrCreate()
l = [('Alice', 1),('Bob', 3)]
df = spark.createDataFrame(l, ['name', 'age'])
df.filter(df.age > 1).collect()
```
show filter results:
```
[Row(name='Bob', age=3)]
```

Jupyter UI
* http://192.168.99.100:8888/lab

Spark UI
* http://192.168.99.100:4040


## Reference 

* https://medium.com/fundbox-engineering/overview-d3759e83969c?mkt_tok=eyJpIjoiTldZME9EQTBPRGszWVRJMSIsInQiOiJvN2dKUDRNTkE5XC80NHUxTFVLWmJwbU8ranR3TjV1UkVySEZTVmFIQlFPS0hwUm04d2cybVo0WVZ3Y3pzeVBQYnY0RlhqR1FQaDNoeDVzcnFWWGpWWEFOM0t6S2NBYTN0emlJTDNWdGNnYUJcL25SaVJsSlZDSlh3aUFVUkJiWlhwIn0%3D