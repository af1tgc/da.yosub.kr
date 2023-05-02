---
title: Configuration of Auditbeat
description: 
published: true
date: 2023-04-24T00:26:24.800Z
tags: security, bigdata, es, elastic-search, auditbeat, auditd
editor: markdown
dateCreated: 2023-03-30T05:52:28.779Z
---

# Auditbeat 설정하기
구성된 ES / Kibana 서버로 감사하고자 하는 시스템 로그를 `auditd` 패키지를 활용하여 전송할 수 있다.
설정은 Auditbeat를 통하여 진행할 수 있으며, 구성은 간단하다.

## Install Auditbeat
[공식 문서](https://www.elastic.co/guide/en/beats/auditbeat/8.6/auditbeat-installation-configuration.html)에 따르면 다음 절차를 통하여 설치를 진행할 수 있다.
```shell
curl -L -O https://artifacts.elastic.co/downloads/beats/auditbeat/auditbeat-8.6.2-linux-x86_64.tar.gz
tar xzvf auditbeat-8.6.2-linux-x86_64.tar.gz
```

## Connect to the Elastic Stack
구성된 Elastic Stack 정보를 auditbeat.yml 파일에 기록한다.
```yml
output.elasticsearch:
  hosts: ["https://$ELASTIC_HOST:9200"]
  username: "elastic"
  password: "$YOUR_PASSWORD" 
  ssl:
    enabled: true
    # fingerprint 는 초기 ES를 구성할때, 화면에 노출된 값이다.
    ca_trusted_fingerprint: "b9a10bbe64ee9826abeda6546fc988c8bf798b41957c33d05db736716513dc9c" 
```

```yml
setup.kibana:
    host: "http://$KIBANA_HOST:5601" 
```

## Set up assets
auditbeat를 설정한 서버에서 다음 명령을 통하여 setup을 진행한다. (기다리면 종료됩니다!)
```shell
./auditbeat setup -e
```

## Start Auditbeat
다음 명령어를 통하여 auditbeat를 실행하면, auditd 로그가 ES 서버로 전송된다.
- 기본 포트는 `8200` `송신`이다.
- auditbeat.yml 파일의 권한은 root로 설정되어 있어야한다.
```shell
sudo ./auditbeat -e
```

실행하면 즉시 auditd 로그 전송이 시작되며, Kibana search 에서 `auditbeat-*` 인덱스로 내용을 확인할 수 있다. 
![스크린샷_2023-03-30_오후_2.54.18.png](/스크린샷_2023-03-30_오후_2.54.18.png)

<br>

## Configuration & Running Background
- auditbeat.yml 파일에서 감사하고자하는 내용을 설정할 수 있다.
- Backgroung Daemon -> & 으로 돌려도 되는가?