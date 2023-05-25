---
title: 명령어 주기적으로 실행하기
description: 
published: true
date: 2023-05-25T09:43:48.007Z
tags: linux
editor: markdown
dateCreated: 2023-05-25T09:43:48.007Z
---

# 명령어 주기적으로 실행하기
```bash
while true; do ps -ef | grep {$KEY_WORD}; sleep 5; done;
```