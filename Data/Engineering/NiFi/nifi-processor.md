---
title: Explanation of NiFi Processor
description: 
published: true
date: 2023-05-12T01:01:25.551Z
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

# EvaluateJsonPath
- flowfile-content의 json을 파싱하여 flowfile-content / flowfile-attribute 로 라우팅해주는 Processor
   - flowfile-content
      - file 개념
      - JVM 온메모리에서 동작하는 것 같다.
      - QueryRecord Processor를 사용하여 쿼리형태로 가공이 가능한 것 같다.
   - flowfile-attribute
      - 메타데이터 개념. 단, 실데이터를 두고 사용할 수도 있다. 
      - 큰 데이터는 Attribute에 넣고 사용하는 것을 권장하진 않는 것 같다.
- 필요한 컬럼만 솎아서 내보낼 수 있다.
- PROPERTIES에서 `+` 선택 후, Property에 Key Value에 Value를 작성하면, 해당 형태로 파싱한다.

# UpdateAttribute
- Attribute의 내용을 Update하는 Processor
- 조건에 따른 속성 업데이트는 아래와 같은 구문으로 사용이 가능하다.
   - `key_name_that_you_want_to_set` : `T`
  > **Property**
  > ```
  > key_name_that_you_want_to_set
  > ```
  > **Value**
  > ```
  > ${keyName:equals('true'):ifElse('T','F')}
  > ```

