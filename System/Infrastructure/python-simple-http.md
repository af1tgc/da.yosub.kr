---
title: Python Simple Http Server
description: 
published: true
date: 2023-04-18T00:50:09.049Z
tags: python, infra, server
editor: markdown
dateCreated: 2023-04-18T00:47:47.635Z
---

# Python SimpleHTTPServer
- python simple http server는 간편하게 파일 공유를 할 수 있다는 장점이 있다.
- 단, 싱글 스레드로 돌아가며 멀티 유저 접속이 불가능하다고 한다.


## Python 2.x
```shell
# python2 -m SimpleHTTPServer {$PORT_NUM}
python2 -m SimpleHTTPServer 8888
```

## Python 3.x
```shell
# python3 -m http.server {$PORT_NUM}
python3 -m http.server 8888
```