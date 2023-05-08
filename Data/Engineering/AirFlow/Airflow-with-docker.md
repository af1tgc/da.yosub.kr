---
title: Airflow with Docker
description: 
published: true
date: 2023-05-08T05:37:41.703Z
tags: dataflow, airflow, docker
editor: markdown
dateCreated: 2023-05-08T05:37:41.703Z
---

# Docker 바이너리 확인
airflow 를 docker로 배포하기 위해서는 docker 및 docker-compose 가 필요하다.

## docker-compose 설치
```shell
wget https://github.com/docker/compose/releases/download/v2.17.3/docker-compose-$(uname -s)-$(uname -m)
sudo mv docker-compose-$(uname -s)-$(uname -m) /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

정상 설치 확인
```shell
docker-compose -v
```

# Docker 로 설치하기
## airflow docker-compose.yaml
```shell
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.6.0/docker-compose.yaml'
```

쉽게 설정하기 위해서, CeleryExecutor 를 LocalExecutor 로 변경하고, redis / airflow-worker / flower 서비스를 내린다.
```yaml
x-airflow-common:
	environment:
		AIRFLOW__CORE__EXECUTOR: LocalExecutor
    # AIRFLOW__CELERY__RESULT_BACKEND: db+postgresql://airflow:airflow@postgres/airflow
    # AIRFLOW__CELERY__BROKER_URL: redis://:@redis:6379/0
  depends_on:
  	# redis:
    # condition: service_healthy

services:
	# redis
	  # 전체 삭제

	# airflow-worker:
	  # 전체 삭제
  
  # flower:
	  # 전체 삭제

```

기본 설정 port 는 8080이며, 외부로 통신하는 포트를 변경하기 위해 호스트 port 바인딩 설정을 변경한다.
```shell
services:
  airflow-webserver:
    ports:
      - "8888:8080"
    healthcheck:
      test: ["CMD", "curl", "--fail", "http://localhost:8080/health"]
```

## docker-compose up
```shell
sudo docker compose up airflow-init
# exit code 0 확인
```

```shell
sudo docker-compose up -d
```

```shell
sudo docker ps
```

완료 후, http://{$AIRFLOW_URL}:8888 로 접속되면 성공