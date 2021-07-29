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

### Setup
`/usr/lib/systemd/system/loki.service`
```
[Service]
ExecStart=/home/cr2/lib/loki/loki-linux-amd64 -config.file /home/cr2/lib/loki/loki-local-config.yaml
```

### Run
```
chmod +x loki-linux-amd64
nohup ./loki-linux-amd64 -config.file=loki-local-config.yaml &
or
nohup ./loki-linux-amd64 -config.file=loki-local-config.yaml > /dev/null &
```

## Promtail

### Download
```
$ wget https://github.com/grafana/loki/releases/download/v2.2.1/promtail-linux-amd64.zip
$ unzip promtail-linux-amd64.zip
$ wget https://raw.githubusercontent.com/grafana/loki/main/clients/cmd/promtail/promtail-local-config.yaml
```

### Run
```
nohup ./promtail-linux-amd64 -config.file=promtail-local-config.yaml &
```