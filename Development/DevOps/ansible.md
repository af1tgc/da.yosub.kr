---
title: Ansible
description: 
published: true
date: 2023-04-19T05:44:02.527Z
tags: development, devops
editor: markdown
dateCreated: 2023-04-19T01:56:44.680Z
---

# Ansible
이 문서는 [Ansible Offical Docs (v7)](https://docs.ansible.com/ansible/latest/) 내용을 정리한 문서입니다.

## Getting started with Ansible
- Ansible은 원격 시스템 관리를 자동화하고 제어한다. 
- 주요 구성요소는 다음과 같다.
  - `Control Node` - Ansible이 설치된 메인 노드
  - `Managed Node` - Ansible로 관리하는 노드
  - `Inventory` - Managed Node의 목록
- 기타 구성요소는 다음과 같다.
  - `playbook` - play 단위의 집합. 실행개념
  - `play` - Ansible 실행을 위한 기본 컨텍스트
  - `role` - Ansible 컨텐츠의 제한된 배포
  - `task` - play에 포함된 작업
  - `handler` - 이전 작업에서 변경된 상태 발생시 알림
  - `module` - 정의된 작업을 수행하기 위해 복사/실행하는 바이너리
  - `plugin` - 핵심 기능 확장
  - `collection` - playbook, role, module, plugin이 포함된 Ansible 컨텐트가 배포되는 형식
  - `AAP` - Ansible 생태계의 도구들을 통합하는 제품 (Ansible Automation Platform)
  
1. [Ansible 설치](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installation-guide)
```python
python3 -m pip install --user ansible
```

2. 원격 시스템의 IP 주소 또는 FQDN을 /etc/ansible/hosts에 추가하여 인벤토리를 생성한다.

```
[myvirtualmachines]
192.0.2.50
192.0.2.51
192.0.2.52
```

> 2-alt-1. 이 단계는 inventory.yaml 파일을 임의의 디렉토리에 구성함으로써 대체가 가능하다.
> **인벤토리 구성의 자세한 내용은 공식 문서 참고.**
> ```yml
> virtualmachines:
>  hosts:
>    vm01:
>      ansible_host: 192.0.2.50
>    vm02:
>      ansible_host: 192.0.2.51
>    vm03:
>      ansible_host: 192.0.2.52
> ```
>
> 2-alt-2. 인벤토리 내용을 검증한다.
> ```shell
> ansible-inventory -i inventory.yaml --list
> ```
>
> 2-alt-3. 핑테스트를 진행한다.
> ```shell
> ansible virtualmachines -m ping -i inventory.yaml
> ```

3. 인벤토리에 호스트가 추가되었는지 확인한다.

```
ansible all --list-hosts
```

```
hosts (1):
  192.0.2.50
  192.0.2.51
  192.0.2.52
```
  
4. Ansible은 SSH를 통하여 Managed node에 연결하기 때문에, SSH 연결을 설정한다.
  - Public SSH Key를 각 원격 시스템의 authorized_keys 파일에 추가한다.
  - SSH 연결 테스트 :

```
ssh username@192.0.2.50
```

제어 노드의 사용자 이름이 호스트에서 다른 경우 ansible 명령에 -u 옵션을 추가해야함

5. Ping 테스트를 진행한다.

```
ansible all -m ping
```

```
192.0.2.50 | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
    }
192.0.2.51 | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
    }
192.0.2.52 | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
    }
```

## Creating a playbook
playbook은 yaml 포멧으로 구성된 자동화 청사진이다.
- `playbook` - managed node를 배포/구성하기 위한 작업 순서가 정의된 play 목록
- `play` - 인벤토리와 매핑된 작업 목록
- `task` - ansible 작업이 정의된 하나 이사의 모듈 목록
- `module` - managed node에서 실행하는 코드 또는 바이너리

1. Control node에서 임의의 디렉토리에 playbook.yaml 파일을 생성하고 다음 내용을 입력한다.

```yml
- name: My first play
  hosts: virtualmachines
  tasks:
   - name: Ping my hosts
     ansible.builtin.ping:
   - name: Print message
     ansible.builtin.debug:
       msg: Hello world
```       

2. playbook을 실행한다.
```shell
ansible-playbook -i inventory.yaml playbook.yaml
```
```
PLAY [My first play] **********************************************************************

TASK [Gathering Facts] ********************************************************************
ok: [vm01]
ok: [vm02]
ok: [vm03]

TASK [Ping my hosts] **********************************************************************
ok: [vm01]
ok: [vm02]
ok: [vm03]

TASK [Print message] **********************************************************************
ok: [vm01] => {
    "msg": "Hello world"
}
ok: [vm02] => {
    "msg": "Hello world"
}
ok: [vm03] => {
    "msg": "Hello world"
}

PLAY RECAP ********************************************************************************
vm01: ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vm02: ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vm03: ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
































