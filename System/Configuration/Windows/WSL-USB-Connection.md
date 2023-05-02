---
title: WSL에 USB 연결하기
description: 
published: true
date: 2023-03-15T07:57:43.600Z
tags: system, windows
editor: markdown
dateCreated: 2023-03-15T07:54:28.172Z
---

# WSL USB Connection

[USB 연결 가이드 - microsoft 공식 문서](https://docs.microsoft.com/ko-kr/windows/wsl/connect-usb)

<br>

## ****USBIPD-WIN 프로젝트 설치****

```powershell
winget install --interactive --exact dorssel.usbipd-win
```

<br>

## ****Linux에서 USBIP 도구 및 하드웨어 데이터베이스 설치****

```powershell
sudo apt install linux-tools-5.4.0-77-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/5.4.0-77-generic/usbip 20
```

<br>

## ****USB 디바이스 연결****

1. *관리자* 모드에서 PowerShell을 열고 명령을 입력하여 Windows 연결된 모든 USB 디바이스를 나열합니다.

    ```
    # PowerShell
    usbipd wsl list
    ```

<br>

2. WSL에 연결하려는 디바이스의 버스 ID를 선택하고 이 명령을 실행합니다. sudo 명령을 실행하려면 WSL에서 암호를 입력하라는 메시지가 표시됩니다. 연결할 Linux 배포판은 기본 배포여야 합니다. 기본 배포를 변경하려면 [WSL용 기본 comands](https://docs.microsoft.com/ko-kr/windows/wsl/basic-commands#set-default-linux-distribution) 문서를 참조하세요.
   
    ```
    # PowerShell
    usbipd wsl attach --busid <busid>
    ```
<br>

3. Ubuntu(또는 원하는 WSL 명령줄)를 열고 다음 명령을 사용하여 연결된 USB 디바이스를 나열합니다.

    ```
    # Bash
    lsusb
    ```
    
    방금 연결한 디바이스가 표시되고 일반 Linux 도구를 사용하여 디바이스와 상호 작용할 수 있어야 합니다. 애플리케이션에 따라 루트가 아닌 사용자가 디바이스에 액세스할 수 있도록 udev 규칙을 구성해야 할 수 있습니다.
<br>

4. WSL에서 디바이스 사용을 완료한 후에는 USB 디바이스의 연결을 물리적으로 끊거나 *관리자* 모드에서 PowerShell에서 이 명령을 실행할 수 있습니다.

    ```
    # PowerShell
    usbipd wsl detach --busid <busid>
    ```