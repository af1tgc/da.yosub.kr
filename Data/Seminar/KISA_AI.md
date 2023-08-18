---
title: KISA AI Dataset
description: 
published: true
date: 2023-08-18T01:51:28.142Z
tags: data
editor: markdown
dateCreated: 2023-08-18T01:07:08.420Z
---

# Summary
데이터셋 수요 조사를 통한 분야 발굴 확장 및 최신-고도화
* 침해사고
	* 실제 사고 재현
  * **[D]** IDS/IPS, WAF, FW, System, EDR
* 악성코드
  * **[D]** exe, apk, dll, hwp, pdf, jpg 등
* 애플리케이션 보안
	* 3rd-party SW : CVE/CWE 식별된 소스코드 및 공격코드
  * **[D]** C/C#, Java, PHP, Python 등
* 위협프로파일링
	* **[D]** IDS/IPS, WAF, FW, System, EDR
* 능동형 보안관제
	* **[D]** IDS/IPS, WAF, FW, System, EDR

API나 ~~데이터제공~~을 통하여 사용 가능함.

# Proposal
AI데이터셋 및 AI응용보안기술 적용을 통한 보안성 강화를 목적
> ### 진행
> 수요발굴 -> 가공/구축 -> 공유/활용

개발된 인공지능 모델
* 2021 : 악성코드/침해사고
  * PE등 실행파일 악성여부 탐지
  * 공격 전술 식별 인공지능 모델
* 2022 : 능동형보안관제/위협프로파일링/어플리케이션보안
	* 웹기반 이상징후(접근) 탐지 모델 : 시계열 데이터
  * 제로데이 취약점 검색 모델
  * 공격그룹, 공격기법 식별 모델
  
## 공개된 데이터셋
* BIG-2015 (Kaggle)
* EMBER (Elasitc)
* UCSB-Packed (California Univ.)
* SOREL-20M (Reversing Labs)
* BODMAS (Illinois Univ.)
* KISA - 1 peta 가 넘는 양...
	* 장점
		* 문서형 악성코드 악성코드 샘플도 데이터가 많음
    * 공격 그룹 프로파일링 기술서
    	* Attack에 활용한 특징을 추출하여 데이터셋 구축
    * 봇넷 그룹 프로파일링 기술서
    	* 현재 기능을 선택하여 VT에서 탐지 안되도록 자동생성

## 활용 예시
* KT - 이메일 보안
  1. 백신 / YARA Rule 교차검증하였지만 신변종 악성코드 지속 발생
  2. 데이터만 활용 : 83 -> 92.6 (%)
* 넥슨 - 게임핵 차단
	1. 악성코드 -> 게임핵 -> 특징추출
	2. 평균 탐지율 96 (%)
* 중소벤처기업부 - 웹보안
	1. 로봇접속, 공격자추적/식별

## 참여방법
* 구축된 데이터셋 자체만 활용
* AI 모델을 활용해서 참여