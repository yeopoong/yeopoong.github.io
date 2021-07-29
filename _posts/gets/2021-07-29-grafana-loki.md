---
layout: post
title: "Log Search with Grafana, Loki and Promtail"
categories: gets
tags: grafana loki promtail
---

## Loki

### Download
```
$ wget https://github.com/grafana/loki/releases/download/v2.2.1/loki-linux-amd64.zip
$ unzip loki-linux-amd64.zip
$ wget https://raw.githubusercontent.com/grafana/loki/master/cmd/loki/loki-local-config.yaml
```

### Run
```
chmod +x loki-linux-amd64
nohup ./loki-linux-amd64 -config.file=loki-local-config.yaml &
or
nohup ./loki-linux-amd64 -config.file=loki-local-config.yaml > /dev/null &
```

### Test

curl -XGET http://localhost:3100/metrics

## Promtail

### Download
```
$ wget https://github.com/grafana/loki/releases/download/v2.2.1/promtail-linux-amd64.zip
$ unzip promtail-linux-amd64.zip
$ wget https://raw.githubusercontent.com/grafana/loki/main/clients/cmd/promtail/promtail-local-config.yaml
```

### Config

`promtail-local-config.yaml`
```
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://localhost:3100/loki/api/v1/push

scrape_configs:
- job_name: system
  static_configs:
  - targets:
      - localhost
    labels:
      job: varlogs
      __path__: /home/cr2/cr2-api/logs/*log
```

### Run
```
nohup ./promtail-linux-amd64 -config.file=promtail-local-config.yaml &
```