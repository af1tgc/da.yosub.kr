---
title: NiFi
description: 
published: true
date: 2023-04-24T02:12:33.093Z
tags: bigdata, dataflow
editor: markdown
dateCreated: 2023-04-24T02:12:31.508Z
---

# NiFi
## Core Concepts
- `FlowFile` - 시스템을 통해 이동하는 각 객체, key:value
- `FlowFile Processer` - 에디터 라우팅, 변환 등. FlowFile 속성 엑세스.
- `Connection` - 프로세서간의 연결, 대기열 개념, 우선순위 부여
- `Flow Controller` - 프로세서간의 연결 관리, 브로커 역할
- `Process Group` - 프로세스 및 연결 집합

### Cons
- 프로세서 흐름 방향의 시각적 직관화
- 비동기 방식으로 매우 높은 처리량과 자연스러운 버퍼링 허용
- 높은 동시성 모델 제공
- 데이터 in/out의 흐름을 쉽게 추적 가능

## Architecture
```
|-OS/Host----------------------------|
|                                    |
| |-JVM----------------------------| |
| |        | WEB Server |          | |
| |                                | |
| |  |--Flow Controller---------|  | |
| |  | | Processer 1 |          |  | |
| |  |       | Extension N |    |  | |
| |  ---Repository--------------|  | |
| |  | FlowFile | | Content |   |  | |
| |  |           | Provenance | |  | |
|------------------------------------|
```

## Getting Started
### Installation
- Linux
  Install with `tar.gz`, [다운로드 링크](http://nifi.apache.org/download.html)
  
- MacOs
  ```shell
  brew install nifi # macos
  ```
	
### Generate Credential
```shell
nifi set-single-user-credentials $USERNAME $PASS
```

### Start
```shell
nifi start # with Configuration with $DIR/nifi.propertiesNiFi.conf
```
