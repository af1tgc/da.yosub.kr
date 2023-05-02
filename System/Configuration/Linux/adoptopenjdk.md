---
title: Install adoptopenjdk 11 with yum command
description: 
published: true
date: 2023-03-31T05:48:36.583Z
tags: system, linux, package, install, jdk, yum, java
editor: markdown
dateCreated: 2023-03-31T05:46:48.540Z
---

# Cent OS에 adoptopenjdk 11 설치하기
1. 레포지토리 추가
```shell
# vi /etc/yum.repos.d/adoptopenjdk.repo 
[AdoptOpenJDK]
name=AdoptOpenJDK
baseurl=http://adoptopenjdk.jfrog.io/artifactory/rpm/centos/$releasever/$basearch
enabled=1
gpgcheck=1
gpgkey=https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public
```

2. yum 설치
```shell
yum install adoptopenjdk-11-hotspot-11.0.11+9-3.x86_64
```

3. 설치 위치
설치된 경로의 bin 및 lib 을 환경변수에 추가해야할 수 있다.
```shell
/usr/lib/jvm/adoptopenjdk-11-hotspot
```