---
title: wail2ban
description: 
published: true
date: 2023-03-15T08:03:11.275Z
tags: system, windows, security
editor: markdown
dateCreated: 2023-03-15T08:01:51.466Z
---

# wail2ban

![untitled.png](/untitled.png)

## 1. 개요

wail2ban은 fail2ban의 기본 기능과 ts_block의 요소를 결합한 Windows 방화벽이다. 
이는 알려진 Event ID를 기반으로 실패한 인바운드 엑세스를 일정 시간동안~~1차 300초, 2차 1500초…~~ 차단하는 임시 방화벽 규칙을 자동 생성한다고 한다.

- RDP(원격데스크탑)과 같은 서비스에 대하여 Brute-force Attack(무차별 대입 공격)을 유용하게 방어할 수 있다.
- PowerShell 스크립트로 작성되어 있다.
- 저작자(Attribution)는 Kaite McLaughlin이며, 라이센스(License)는 BSD 3-Clause License를 따른다.

wail2ban은 [https://github.com/glasnt/wail2ban](https://github.com/glasnt/wail2ban)에서 다운로드 받을 수 있다.

<br>

## 2. 설치

1.  C:\scripts\wail2ban 폴더 생성 후, [Github Repository](https://github.com/glasnt/wail2ban) 내 파일을 저장한다.
2.  작업스케쥴러(Task Scheduler)에 onstartup.xml을 임포트한다.
3.  start_wail2ban.bat 파일을 실행한다.

<br>

## 3. 동작

일반적으로 RDP 보안은 VPN 사용 혹은 기본 포트 변경을 권장하나, 네트워크 대역에서의 보안장비가 없고 어디서나 원격연결이 필요한 사용자는 wail2ban 사용을 적극 고려하는 편이 좋아보인다. ~~아무리 기본 포트를 변경한다고해서 100% 안전한 것은 아니기 때문에~~

원격 데스크톱 연결 사용을 하다보면 아무리 포트(3389 to x)를 변경하여 사용하더라도 어느순간 1~2초 단위로 접속시도 
로그가 기록된다. 
원격 데스크톱 연결 시도 로그는 `[응용 프로그램 및 서비스 로그 > Microsoft > Windows > TerminalServices-RemoteConnectionManager > Operational]` 에서 확인할 수 있으며 위와 같은 로그를 직면하게 되면 사용자는 공포심에 휩싸이게될 가능성이 농후하다.
물론 `[TerminalService-LocalSessionManager > Operational]`에 성공 세션 기록을 확인해 침해를 당하지 않았음을 확인할 수 있지만, 가능성 조차 막아주는 것이 데이터를 지키는 첫 걸음임을 명심하자.

wail2ban을 사용하면 위와 같은 상황을 미연에 방지할 수 있다. 정해진 규칙에 따라 실패 감사가 몇 회이상 기록되면 자동으로 윈도우 방화벽 규칙에 등록된다. 
물론 Expire Time이 함께 적용되므로 불안하다면 DEBUG Log내 IP를 `[방화벽 > 고급설정 > 인바운드 규칙]`에서 영구 차단하도록 하자.

만약 사용자가 실수로 정책에 걸렸다면 ~~정말 극히 드문 경우다. 틀리고 또, 틀리고 금붕어인가~~ 로컬 로그인 후 `[방화벽 > 고급설정 > 인바운드 규칙]`에서 간단하게 규칙을 삭제해주면 된다.
또한, wail2ban을 더이상 사용하고 싶지 않다면 작업스케쥴러(Task Scheduler)에서 onstartup.xml을 삭제하면된다.

<br>

## 4. 여담

- 물론 패스워드는 3가지 조합 25자리 이상 사용하도록하자. 🤣
    
- RDP 접속에 대한 감사 실패 로그는 `[Windows 로그 > 보안]`에 남는다. 여기서 원격지 접속 시도 IP를 확인할 수 있으므로 수동으로 차단하려면 해당 로그를 확인하자! `(Event ID : 4625)`