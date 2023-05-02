---
title: Big-Data
description: 
published: true
date: 2023-03-30T01:21:53.006Z
tags: bigdata, engineering, data
editor: markdown
dateCreated: 2023-03-24T06:51:33.130Z
---

# Big-Data

## Data Format
- 정형
  - csv, database, ...
- 반정형
  - XML, json, html. ...
- 비정형
  - audio, Natural Language, ...
  
<br>

## Ecosystem
<br>

### Data Collection
- Flume (by Cloudera)
  - Agent(Source, Channel, Sink) -> HDFS
- Fluentd (by Treasure Data)
  - Agent(Input, Buffer, Output) -> HDFS
- Kafka (by Linkedin)
  - Publish -> `MQ` <- Subscribe
- NiFi (by NSA)
  - System1 -> `DATA FLOW` -> System2
- Sqoop
  - RDBMS -> HDFS
<br>

### Workflow Management Platform
- Airflow (by Airbnb)
  - Can attach with `Hive`, `presto`, `DBMS engine`
- Azkaban (by Linkedin)
- Oozie

<br> 

### Serialization
- Avro
- Thrift
- Protocol Buffers

<br> 

### Storage
- HDFS
- S3
- Data Lake
- Cloud Storage

<br> 

### Distributed Query Engine
- Hive
- Presto
- Impala
- Spark
- Drill
- Tajo
- Pig

https://www.linkedin.com/pulse/10-distributed-sql-queryengine-big-data-kumar-chinnakali/

<br> 

###

<br> 

###

<br> 

###

<br> 

###