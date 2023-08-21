---
title: Airflow - Add Python Packages
description: 
published: true
date: 2023-08-21T06:36:10.456Z
tags: engineering, data, dataflow, airflow
editor: markdown
dateCreated: 2023-08-21T06:35:42.851Z
---

# Airflow Container에 Python Package 추가하기
1. Host PC의 Project 디렉토리에 접근하여 `requirements.txt` 파일을 작성한다.
```
pymysql
```

2. Host PC의 Project 디렉토리에 `Dockerfile`을 작성한다.
```Dockerfile
FROM apache/airflow:2.6.0
COPY requirements.txt /requirements.txt
RUN pip install --user --upgrade pip
RUN pip install --no-cache-dir --user -r /requirements.txt
```

3. 생성한 `Dockerfile`을 활용하여 빌드한다.
```bash
docker build . --tag extending_airflow:latest
```


4. 빌드한 이미지 `docker-compose.yaml`에 정의하여 활용한다고 설정한다.
```yaml
version: '3.8'
x-airflow-common:
  &airflow-common
  #image: ${AIRFLOW_IMAGE_NAME:-apache/airflow:2.6.0}
  image: ${AIRFLOW_IMAGE_NAME:-extending_airflow:latest}
  # build: .
```

5. webserver 및 scheduler 를 up 한다.
```bash
docker-compose up -d --no-deps --build airflow-webserver airflow-scheduler
```