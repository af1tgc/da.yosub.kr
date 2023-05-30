---
title: Run n8n as a Service
description: 
published: true
date: 2023-05-30T05:45:37.868Z
tags: engineering, data, n8n
editor: markdown
dateCreated: 2023-05-30T05:45:37.868Z
---

> https://community.n8n.io/t/run-n8n-as-a-service-with-pm2/1199

# 가정 및 시스템 환경
이 문서에서는 다음을 가정합니다.

- 시스템에 실행 중인 n8n 사본이 있습니다.
- 시스템에 대한 SSH/터미널 액세스 권한이 있습니다.
- 애플리케이션 설치를 위해 시스템에 대한 루트/sudo/admin 액세스 권한이 있습니다.

이 문서는 2020년 4월 21일 현재 최신 업데이트로 완전히 패치된 Ubuntu 18.04 VM을 사용하여 작성되었습니다. 시스템에는 듀얼 CPU, 4GB RAM 및 16GB HDD가 있습니다.

# PM2 설치
PM2의 놀라운 점은 NodeJS 응용 프로그램이라는 점입니다. 따라서 NodeJS 응용 프로그램으로 작업하는 것이 편하다면(n8n을 실행하고 있기 때문이라고 가정합니다) PM2 설치는 간단해야 합니다! 다음 단계를 따르십시오.

1. n8n 서버에 대한 터미널 또는 SSH 세션에 로그인합니다.
2. 다음 명령을 실행합니다.
```bash
npm install pm2@latest -g
```
이제 시스템에 PM2가 설치되어 있어야 합니다.

# PM2로 n8n 실행
PM2와 함께 n8n을 실행하려면 다음 명령을 입력하십시오.

```bash
pm2 start n8n
```

# 부팅 시 n8n 자동 시작
n8n을 서비스처럼 실행하는 것의 또 다른 놀라운 점은 시스템이 재부팅되면 언제든지 시작할 수 있다는 것입니다. 즉, 시스템이 백업되어 실행되자마자 n8n도 마찬가지입니다.

PM2와 함께 n8n을 실행하면 다음 두 명령을 실행하여 자동 시작하도록 구성할 수 있습니다.

```shell
pm2 startup
pm2 save
```

첫 번째 명령은 시작 스크립트를 생성하는 명령을 실행하라는 메시지를 표시합니다.

두 번째 명령은 다음에 시스템을 재부팅할 때 자동으로 실행되도록 시작 스크립트를 저장합니다.

# n8n 서비스 관리
이제 n8n이 실행 중이고 자동 실행 서비스로 적절하게 구성되었으므로 n8n을 최상의 상태로 계속 실행할 수 있도록 서비스로 몇 가지 기본적인 유지 관리 작업을 수행하는 방법을 알아야 합니다.

## n8n 서비스 중지
```bash
pm2 stop n8n
```
## n8n 서비스 재시작
```bash
pm2 restart n8n
```
## n8n 서비스 새로 고침
```bash
pm2 reload n8n
```
## n8n 서비스 제거
```bash
pm2 delete n8n
```
## PM2 서비스 나열
```bash
pm2 list
```
## PM2 로그 표시
```bash
pm2 logs
```
pm2 logs --lines 100명령을 사용하여 마지막 100줄만 표시할 수도 있습니다 . 100원하는 모든 숫자가 될 수 있습니다.

# n8n 서비스 모니터링
pm2가 실행 중인 n8n 서비스를 모니터링할 수 있는 두 가지 주요 방법이 있습니다. 터미널 대시보드 사용 또는 pm2.io 사용 125웹사이트.

## 터미널 대시보드
터미널 대시보드를 실행하려면 다음 명령을 사용하십시오.

```bash
pm2 monit
```
이렇게 하면 프로세스, 로그, 사용자 지정 메트릭 및 애플리케이션 메타데이터에 대한 정보가 포함된 네 개의 상자가 화면에 표시됩니다.

# Refs
## pm2.io
pm2.io _ 125웹사이트는 n8n이 수행하는 작업에 대한 완전한 웹 인터페이스를 제공합니다. 사용하려면 다음을 수행해야 합니다.

1. pm2.io 로 이동
2. 계정 만들기
3. 서버의 PM2 관리자를 pm2.io 에 연결
4. 예쁜 그래프 모두 즐겨보세요

이를 수행하는 방법에 대한 자세한 내용은 웹 대시보드 빠른 시작 설명서를 확인하세요.

## 구성에 도움이 될 수 있는 기타 유용한 문서:

[PM2 빠른 시작](https://pm2.keymetrics.io/docs/usage/quick-start/)
[PM2 기록](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/)
[GitHub의 PM2](https://github.com/Unitech/pm2)
[pm2.io에 계정 등록](https://id.keymetrics.io/api/oauth/register)