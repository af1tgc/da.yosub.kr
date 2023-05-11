---
title: Airflow Example DAGs
description: 
published: true
date: 2023-05-11T06:55:23.292Z
tags: engineering, data, airflow, batch
editor: markdown
dateCreated: 2023-05-11T06:55:23.292Z
---

# AIRFLOW DAG 예시 

- 본 예시는 AIRFLOW POC 간 작성한 코드임. 
- API CALL 기능 테스트를 포함함
- 분기처리 동작 테스트를 포함함

```python
from datetime import datetime, timedelta
import requests
import json
import time

from airflow import DAG
from airflow.operators.python import PythonOperator
from airflow.operators.python import BranchPythonOperator

from airflow.providers.http.hooks.http import HttpHook
from airflow.hooks.base_hook import BaseHook
from airflow.models.connection import Connection

from airflow.providers.http.operators.http import SimpleHttpOperator
from airflow.providers.http.sensors.http import HttpSensor

import tenacity
from tenacity import *


default_args = {
    'owner': 'admin',
    'retry': 1,
    'retry_delay': timedelta(minutes=1)
}


# USE NATIVE REQUEST MODULES FOR API CALL.
def get_ticket():
    params = {'pageNumber': '0', 'pageSize': '1'}
    headers = {'Content-Type': 'application/json', 'Authorization': token}

    res = requests.get(URL, params=params, headers=headers)
    print(res.text)

    body = json.loads(res.text)
    print(body["result"]["content"])

    return body["result"]["content"][0]


# USE AIRFLOW CLASS FOR API CALL, YOU MUST SET THE CONNECTIONS ON WEB PAGE.
"""
def get_handler():
    print("start")

    conn = HttpHook(method="POST", http_conn_id="naver_ping")
    sess = conn.get_conn()

    rt = dict(
        wait=tenacity.wait_exponential(),
        stop=tenacity.stop_after_attempt(1),
        retry=tenacity.retry_if_exception_type(Exception),
    )

    res = conn.run_with_advanced_retry(endpoint='', _retry_args=rt)
    print(res.text)

    # conn.run_and_check()
    # conn.check_response(response=)
    # conn.run(endpoint="", data="", headers="", extra_options={'check_response':False})

    print("ticket ends")
"""


# 1. USAGE OF THE XCOM : USE {$TASK_NAME}.task_id FOR ASSIGN THE RETURN VALUE OF {$TASK_NAME}
# 2. BRANCH : `BranchPythonOperator` MEANS THE FUNCTION HAS CONDITION TO BRANCH : RETURN THE {$TASK_NAME}.task_id
def condition(ti):
    element = ti.xcom_pull(task_ids=get_ticket.task_id)

    if(element['condition'] == 'T'):
        return true_process.task_id
    else:
        return false_process.task_id


def true_process(ti):
    element = ti.xcom_pull(task_ids=get_ticket.task_id)

    params = {'assignId': 'yosub.song'}
    headers = {'Content-Type': 'application/json', 'Authorization': token}

    # res = requests.put(URL, params=params, headers=headers)
    print("TODO 접수 절차 진행")


def false_process():
    print("FALSE (FOR SAMPLE)")


def set_ticket():
    print("SETTING TICKET")


def pass_ticket():
    print("Notting to do...")


with DAG(
    default_args=default_args,
    dag_id="basic_ticket_process_v1",
    start_date=datetime(2023, 4, 28, 14),
    schedule_interval='@daily',
    catchup=False
) as dag:
    get_ticket = PythonOperator(
        task_id='get_ticket',
        python_callable=get_ticket,
        dag=dag
    )

    condition = BranchPythonOperator(
        task_id='condition',
        python_callable=condition,
        dag=dag
    )

    true_process = PythonOperator(
        task_id='true_process',
        python_callable=true_process,
        dag=dag
    )
    false_process = PythonOperator(
        task_id='false_process',
        python_callable=false_process,
        dag=dag
    )
    set_ticket = PythonOperator(
        task_id='set_ticket',
        python_callable=set_ticket,
        dag=dag
    )
    pass_ticket = PythonOperator(
        task_id='pass_ticket',
        python_callable=pass_ticket,
        dag=dag
    )

		# 1. USE [] BRACETs FOR BRANCH, OTHERWISE IT MEANS RUN TASK TO PARALLEL.
    # 2. AFTER BRANCH TASKs, WRITE THE CODE WITH SPERATED LINES.
    get_ticket >> condition >> [true_process, false_process]
    true_process >> set_ticket # IF TRUE, THEN SKIP `false_process`
    false_process >> pass_ticket # IF FALSE, THEN SKIP `true_process`
```