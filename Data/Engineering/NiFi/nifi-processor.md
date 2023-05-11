---
title: Explanation of NiFi Processor
description: 
published: true
date: 2023-05-11T07:08:40.346Z
tags: engineering, data, dataflow, nifi
editor: markdown
dateCreated: 2023-05-11T07:08:40.346Z
---

# GetHTTP
- Get Method Call을 진행하는 Processor
- URL, Filename을 지정하고 기타 필수 인자 값 설정이 필요함
- 추가 Header의 경우, PROPERTIES의 `+` 버튼 클릭 후 추가할 수 있다.

# SplitJson
- JSON Array를 Split 해주는 Processor
- Array가 있는 값을 $.key1.key2 와 같은 형식으로 설정해주면 된다.

# ControlRate
- 후속 프로세서로 전송되는 속도를 제어해주는 Processor
- PROPERTIES 및 RELATIONSHIPS(Failure)를 설정해주면 된다.

# JoltTransformJSON
- JSON의 구조를 변경해주는 Processor
- 원본 JSON 구조에 변환하고자하는 Key를 작성하여 설정하면 된다.

