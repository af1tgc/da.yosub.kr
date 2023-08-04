---
title: 명령어 주기적으로 실행하기
description: 
published: true
date: 2023-08-04T05:12:42.780Z
tags: linux, ps, command
editor: markdown
dateCreated: 2023-05-25T09:43:48.007Z
---

# 명령어 주기적으로 실행하기
```bash
while true; do ps -ef | grep {$KEY_WORD}; sleep 5; done;
```

여기에 clear까지 넣어주면 좋습니다. (ps -ef 로 주기적인 모니터링 진행)
```bash
while true; do ps -ef | grep {$KEY_WORD}; sleep 5; clear; done;
```