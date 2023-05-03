---
title: Airflow
description: 
published: true
date: 2023-05-03T06:26:09.655Z
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

## Maria DB 연동
### Maria DB 설치 
JSON type 사용으로 버젼에 유의가 필요함
```shell
curl -LsS -O https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
```

```shell
sudo bash mariadb_repo_setup --mariadb-server-version=10.9
```

```shell
sudo yum makecache fast
```

```shell
sudo yum -y install MariaDB-server MariaDB-client MariaDB-backup
```

```shell
sudo rpm -qi MariaDB-server
```

```shell
sudo systemctl enable --now mariadb
```

```shell
sudo mariadb-secure-installation
```

### Maria DB 설정
sql_alchemy_conn 설정에 encoding 을 설정해주지 않으면, 다음 에러 발생 `(2019, "Can't initialize character set utf-8 (path: /usr/share/mysql/charsets/)")`

#### utf-8 character-set 설정
```shell
# sudo vi /etc/my.cnf.d/client.cnf

[client]
default-character-set=utf8
```

```shell
# sudo vi /etc/my.cnf.d/mysql-clients.cnf

[mysql]
default-character-set=utf8

[mysqldump]
default-character-set=utf8
```

```shell
# sudo vi /etc/my.cnf.d/server.cnf

[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8

[mariadb]
character-set-client-handshake=FALSE
init_connect="SET collation_connection = utf8_general_ci"
init_connect="SET NAMES utf8"
character-set-server = utf8
collation-server = utf8_general_ci
```

```shell
sudo systemctl restart mariadb.service
```

---

```shell
mysql -u root -p
```

```sql
create database airflow;
grant all privileges on airflow.* to root@localhost;
flush privileges;
```

---

```shell
# vi $AIRFLOW_HOME/airflow.cfg

[database]
sql_alchemy_conn = mysql://root:{$PASSWORD}@localhost:3306/airflow?charset=utf8mb3
sql_engine_encoding = utf8
```

```shell
airflow db init
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

## Daemonize

```shell
cd /etc/systemd/system
```

```shell
# sudo vi airflow-webserver.service

[Unit]
Description=Airflow webserver daemon
After=network.target mysql.service
wants=mysql.service

[Service]
Environment="PATH=/home/centos/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
User=ubuntu
Group=ubuntu
Type=simple
ExecStart=$AIRFLOW_HOME/airflow webserver -p 8080
Restart=on-failure
RestartSec=5s
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

```shell
sudo vi airflow-scheduler.service

[Unit]
Description=Airflow webserver daemon
After=network.target mysql.service
wants=mysql.service

[Service]
Environment="PATH=/home/centos/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
User=ubuntu
Group=ubuntu
Type=simple
ExecStart=$AIRFLOW_HOME/airflow scheduler
Restart=on-failure
RestartSec=5s
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl daemon-reload
sudo systemctl enable airflow-webserver
sudo systemctl enable airflow-scheduler
```

```shell
sudo systemctl start airflow-webserver
sudo systemctl start airflow-scheduler
```

```shell
sudo systemctl status airflow-webserver
```