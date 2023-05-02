---
title: Ansible Security Automation
description: 
published: true
date: 2023-04-19T06:31:46.895Z
tags: devops, ansible
editor: markdown
dateCreated: 2023-04-19T06:31:45.293Z
---

# Ansible Seucurity Automation
## 보안 자동화의 기술적 어려움
- 타이밍
  - 여러 벤더의 다양한 제품 사용에 따라 위협 추적 및 보안 현황을 한눈에 파악하기 어려움
  - 수 많은 GUI 화면을 클릭해야함
- 오류
  - 변경 추적, 로그인 리포지토리 설정 등 수동으로 설정하면 실패의 여지가 있음

## Security Automation 사용 예시

어플리케이션에 위협의 조짐이 확인된 상황을 가정
1. 상황 파악
   - 터미널에서 제어가 필요한 타겟 머신에 바로 로그인 가능
   - 로그인 후, 로그 확인
2. 보안장비 (FW, IDS) 에서 추가 로그 수집이 필요함
   - 하나의 도구에 모아서 상관관계를 파악하는 것이 필요
   - 로그를 모아서 SIEM에 넣는 것이 필요함
    - 많은 사람, 많은 팀의 협업이 필요 > 자동화가 필요

  > **모든 로그를 SIEM에 보내면 안되는 이유?**
  > - 방화벽, 라우터 서버 등 환경내 모든 시스템이 로그를 전송하면 대역폭이 포화될 수 있고 이에 따라, SIEM에서 병목이 발생할 여지가 있음
  > - 불필요한 로그가 포함될 수 있음

3. 2의 절차를 Playbook을 통하여 자동화할 수 있음
   - 로그 전송을 위한 playbook 구성
     - IDS (snort) -> QRadar
     - FW -> QRadar
   - IDS/FW는 선 구성된 설정을 바탕으로 간단하게 보낼 수 있음 : Role 사용
   - QRadar는 IDS에서 로그가 온다는 것을 알 수 있음 : Collection 사용

4. Playbook 실행
```
ansible-playbook enrich_log_sources.yml
```
   - 자동으로 정의된 Task를 수행
   - SIEM에서 정의된 로그를 선별하여 확인

5. IDS에 정책 자동 배포
   - playbook에 소스IP/Port, 목적지IP/Port, Protocol 등을 정의하여 실행하면 모든 IDS에 한번에 룰을 배포할 수 있음
   - reboot이 필요한가? 등에 내용을 사전에 정의할 수 있어 사전지식 없이도 쉽게 배포 가능함
   > 이 절차 내에서는 IDS에 새로운 정책을 배포하여 현재 진행되고 있는 공격이 탐지되도록 구성하기 위함이었음
   
6. 정책 롤백
   - 오탐 혹은 불필요시, 생성한 정책의 롤백이 필요
   - 기존 생성했던 playbook을 활용하여 쉽게 삭제 가능함
   - 예, `state:present` -> `absent` / `ids_config_remote_log:true` -> `false`

## Ansible Tower
- 미리 구성된 playbook을 공유하고 공동 관리할 수 있음
- 권한에 따라 확인할 수 있는 구성을 제한할 수 있음
   - Template Create / View / Execution 등
- **playbook을 ansible tower에서 바로 실행할 수 있음**
- 작업 History를 확인할 수 있음
- IDS룰 추가를 위한 작업 템플릿을 구성할 수 있음