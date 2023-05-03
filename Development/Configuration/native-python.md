---
title: Change Version of Native Python
description: 
published: true
date: 2023-05-03T02:17:04.219Z
tags: configuration, linux, python
editor: markdown
dateCreated: 2023-05-03T01:52:42.660Z
---

# Cent OS

```shell
sudo yum update -y
```

```shell
sudo yum groupinstall "Development Tools" -y
sudo yum install openssl-devel libffi-devel bzip2-devel -y
```

```shell
sudo yum install wget -y
```

```shell
wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz

```

```shell
tar xvf Python-3.10.0.tgz
```

```shell
cd Python-3.10.0
```

```shell
./configure --enable-optimizations
```

```shell
sudo make altinstall
```


```shell
alternatives --install /usr/bin/python python /usr/bin/python2 50
sudo alternatives --install /usr/bin/python python /usr/local/bin/python3.10 70
sudo alternatives --config python
```


```shell
# shell profile에 추가하여 접속시 alias 설정
alias pip=pip3.10
```

```shell
sudo vi /usr/bin/yum

# Change 1st line
#! /usr/bin/python2
```


```shell
sudo vi /usr/libexec/urlgrabber-ext-down

# Change 1st line
#! /usr/bin/python2
```
