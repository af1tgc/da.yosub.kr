---
title: Bloomberg News to Slack
description: 
published: true
date: 2023-05-31T12:46:44.474Z
tags: engineering, data, dataflow
editor: markdown
dateCreated: 2023-05-31T12:46:44.474Z
---

# N8N - Bloomberg 뉴스 수집기
구글에서 블룸버그 뉴스를 수집하여 40분 간격으로 slack에 기사를 전송하는 Workflow를 구성하였다.
전체 흐름은 아래 사진과 같다.
![n8n.png](/n8n.png)

## 구성간 어려웠던 점
- json array를 list화하고 단일화 하는 과정에서 Reference 부족으로 시간이 많이 소요되었다.
- 구글 Translate와 네이버 Papago로 Headline을 번역하여 Slack으로 Hook하는데, 생각보다 번역 API 사용량이 부족하다.
   - 현재는 Papago를 선택했으며, 계정당 10개의 어플리케이션 (총 100,000자) 까지 무료로 사용이 가능한 상태이다.
   - Bloomberg 기사 수집에만 40,000자를 사용하는 수준이며, 직접 번역기를 개발하는 방향을 생각해봐야겠다 (ㅠㅠ)
- Split in Batches 가 단일 테스트간 직관적이지 않다.
   - 단일 Run으로 동작하게되면 다음 batch step에서 마지막 최종 출력 값이 input으로 들어가는 현상이 보였다.
   - 하지만, 전체 `Execute Run`으로 동작하게 되면 정상 배치가 동작함을 확인할 수 있었다.
   
## 소감
- n8n은 js 기반의 코딩으로 꽤나 높은 확장성을 도모하고 있었다.
- 다른 도구와 비교하자면, Airflow > n8n > NiFi 순으로 확성성이 높다.
- 다만, GUI로 편집하고 단일 노드들의 설정이 직관적인것이 코드와 친하지 않은 사람도 쉽게 접근이 가능해보인다.
   - HTML 파싱 과정도 CSS Selector로 쉽게 추출 -> 리스트 변환이 용이하였다.
   - 여러가지 Application들과의 연동을 기본적으로 제공해주고 있어서 slack hook 작성도 용이하였다.
   - 파일 저장 및 json 변환도 손쉽게 이루어졌다.
   
## 고민점
이렇게 구성한 이유는 세계의 모든 뉴스를 최대한 빠르게 접하고 싶다는 이유도 있었지만, (feat. [`슈카월드`](https://www.youtube.com/@syukaworld))
사실 ETF 가격에 영향을 많이 주는 요소가 무엇인지 분석해보기 위함이었다.
따라서, 일별로 수집한 뉴스기사를 저장해야하는 요구가 있지만, 도대체 어디에 저장해야할까?
   - `Google Drive` 에 저장해보고자 했지만...
   - `Dropbox`(?) 기본 제공 용량이 많이 부족하다.. (`2GB`)
   - `Dynamo DB` json 형태이기 때문에 좋아보이나, 완전 무료를 원한다..
   - `ES` 그냥 서버를 사서 ELK 구성하고 뽕을 뽑아?
   
흠......