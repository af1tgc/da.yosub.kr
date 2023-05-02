---
title: Conda Command
description: 
published: true
date: 2023-04-28T04:48:18.189Z
tags: python, env, virtual
editor: markdown
dateCreated: 2023-04-28T04:48:16.600Z
---

# Commands

conda 가상환경 조회

```bash
conda env list
```

conda 가상환경 실행 & 종료

```bash
# 가상환경 실행
conda activate {$ENV_NAME} # 가상환경 종료
conda deactivate
```

conda 가상환경 내 package 목록/버전 확인

```bash
conda list -n {$ENV_NAME}
```

conda 가상환경 생성(create)

```bash
conda create --name {$ENV_NAME}
```

특정 python version의 conda env 생성

```bash
conda create -n {$ENV_NAME} python=3.8
```

특정 conda env을 복제(clone)해 conda env 생성

```bash
conda create --name {$ENV_NAME} --clone {$ENV_NAME}
```

conda 가상환경 제거(remove)

```bash
conda remove --name {$ENV_NAME} --all
```