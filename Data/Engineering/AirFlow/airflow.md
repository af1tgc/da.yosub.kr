---
title: Airflow
description: 
published: true
date: 2023-05-03T06:04:47.749Z
tags: engineering, data, dataflow
editor: markdown
dateCreated: 2023-04-28T05:05:13.715Z
---

# Airflow
## Installation
[Airflow github](https://github.com/apache/airflow) 에서 설치 명령어를 복사한다.
- gcc 사전 설치가 필요.
- python 3.6 이상 필요.
```shell
pip install 'apache-airflow==2.5.3' \
 --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.5.3/constraints-3.7.txt"
```

환경 설정 및 로컬 DB 초기화를 수행한다.
- AIRFLOW_HOME 환경변수는 abs path가 필요하였음
```shell
export AIRFLOW_HOME={$AIRFLOW_DIRECTORY} # 디렉토리는 직접 설정이 필요함
airflow db init
```

Airflow Scheduler를 실행한다.
```shell
airflow scheduler
#inline으로 동작하는 방법이다. Production Daemonize는 추후 업데이트
```

Airflow USER를 생성하고 webserver를 시작해본다.
```shell
airflow users create \
				--username admin \
				--firstname yosub \
				--lastname song \
				--role Admin \
				--email test@example.kr
```

```shell
airflow webserver -p 8988
```

airflow.cfg 파일에서 dags의 디렉터리를 지정해줄 수 있으며, 동파일의 load_example를 False로 설정해주면 샘플 파일이 노출되지 않는다.
```shell
vi $AIRFLOW_HOME/airflow.cfg
```
```
# airflow.cfg
	...
dags_folder = {$}/dags
	...
load_examples = False
	...
```

## Airflow API Enable
```
[api]
# auth_backend = airflow.api.auth.backend.deny_all
auth_backend = airflow.api.auth.backend.basic_auth
```

## Run DAGs
```shell
curl -X POST  \
	'http://0.0.0.0:8988/api/v1/dags/{$DAG_ID}/dagRuns' \
	--user "admin:{$PASSWORD}" \
	--header 'Content-Type: application/json' \
	--header 'Cache-Control: no-cache' \
	--data '{"conf": { }}'
```