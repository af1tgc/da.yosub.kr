---
title: Installation of Elastic Stack
description: 
published: true
date: 2023-04-24T00:25:56.802Z
tags: bigdata, es, elastic-search
editor: markdown
dateCreated: 2023-03-30T01:21:27.273Z
---

# Cent OS에 Elastic Stack 설치하기
Elastic Stack 설치는 다음 포멧을 지원한다.
- tar.gz
- zip
- deb
- rpm 
- docker

본 문서에서는 tar.gz로 직접 설치하는 과정을 다루고자 한다.

# Elastic Search 설치
[공식 문서](https://www.elastic.co/guide/en/elasticsearch/reference/8.6/targz.html)에 따르면 다음 절차를 통하여 설치를 진행할 수 있다.

## Download and install archive for Linux
```shell
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.2-linux-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.6.2-linux-x86_64.tar.gz.sha512
shasum -a 512 -c elasticsearch-8.6.2-linux-x86_64.tar.gz.sha512 
tar -xzf elasticsearch-8.6.2-linux-x86_64.tar.gz
cd elasticsearch-8.6.2/ 
```

## Enable automatic creation of system indices
Auto Index 구성이 필요한 경우, 다음 절차를 진행한다.
```shell
# vi elasticsearch.yml
action.auto_create_index: .monitoring*,.watches,.triggered_watches,.watcher-history*,.ml*
```

## Run Elasticsearch from the command line
시작! ~~이렇게 된다고?~~
*- es 실행은 root 권한으로 실행되지 않는다.*
```shell
./bin/elasticsearch
```

처음 실행시키면, 패스워드 설정 및 Kibana 인증 토큰이 노출된다.
```shell
The generated password for the elastic built-in superuser is:
<password>

The enrollment token for Kibana instances, valid for the next 30 minutes:
<enrollment-token>

The hex-encoded SHA-256 fingerprint of the generated HTTPS CA DER-encoded certificate:
<fingerprint>

You can complete the following actions at any time:
Reset the password of the elastic built-in superuser with
'bin/elasticsearch-reset-password -u elastic'.

Generate an enrollment token for Kibana instances with
'bin/elasticsearch-create-enrollment-token -s kibana'.

Generate an enrollment token for Elasticsearch nodes with
'bin/elasticsearch-create-enrollment-token -s node'.
```

다른 클러스트를 붙이고자 한다면, 다음 명령어를 참고!
```shell
bin/elasticsearch-create-enrollment-token -s node
bin/elasticsearch --enrollment-token <enrollment-token>
# config/certs 에 자동으로 cert 생성
```

## Check that Elasticsearch is running
새로운 터미널을 열고, 포그라운드에서 돌고있는 ES에 다음 명령어를 활용하여 접속해본다.
```shell
curl --cacert $ES_HOME/config/certs/http_ca.crt -u elastic https://localhost:9200 
```
예시🚀
![스크린샷_2023-03-30_오전_10.11.12.png](/스크린샷_2023-03-30_오전_10.11.12.png)

## Run as a daemon
포그라운드에서 확인이 되었으면, 데몬으로 실행시켜 서비스를 해보자!
```shell
./bin/elasticsearch -d -p pid
```

# Kibana 설치
[공식 문서](https://www.elastic.co/guide/en/kibana/8.6/targz.html)에 따르면 다음 절차를 통하여 설치를 진행할 수 있다.

## Download and install the Linux 64-bit package
```shell
curl -O https://artifacts.elastic.co/downloads/kibana/kibana-8.6.2-linux-x86_64.tar.gz
curl https://artifacts.elastic.co/downloads/kibana/kibana-8.6.2-linux-x86_64.tar.gz.sha512 | shasum -a 512 -c - 
tar -xzf kibana-8.6.2-linux-x86_64.tar.gz
cd kibana-8.6.2/ 
```

## Run Kibana from the command line
```shell
./bin/kibana
```

## Remote Access
원격지 접속을 위해서는 다음 설정을 적용해야한다.
```shell
# vi $KIBANA_HOME/config/kibana.yml
server.host: "0.0.0.0"
```

## Configure Elastic to get started
[Run Kibana from the command line](##run-kibana-from-the-command-line) 단계의 명령의 결과로 임시 url이 노출된다. Remote 설정을 하였다면 서버에 주어진 주소로 바꿔서 접속하면 [Run Elasticsearch from the command line](##-run-elasticsearch-from-the-command-line) 에서 노출된 kibana 임시 토큰으로 연결할 수 있다.

<br>
<br>
<br>

> 30분 인증 시간이 초과하였다면?
토큰을 재발급 받고, 다시 연동하면 된다.

### Reissue enrollment token for kibana
**es 노드가 활성화되어 있는 상태**에서 다음 명령어를 실행하면 토큰을 재발급 받을 수 있다.
```shell
./bin/elasticsearch-create-enrollment-token --scope kibana
```

브라우저의 kibana에 토큰을 붙여넣으면 연동이 진행되며, verification code를 입력 창이 노출된다.
kibana 로그에 코드를 붙여넣으면 완료!