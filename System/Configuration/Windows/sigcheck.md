---
title: sigcheck
description: 
published: true
date: 2023-05-11T06:05:50.411Z
tags: security, hash, integrity
editor: markdown
dateCreated: 2023-05-11T06:05:50.411Z
---

# file hash for windows

- sysinternals, `sigcheck.exe` : [download](https://learn.microsoft.com/ko-kr/sysinternals/downloads/sigcheck)
```bat
sigcheck.exe -vt -h {$FILE_PATH}
```

- included tool
```bat
CertUtil -hashfile {$FILE_PATH} md5
```