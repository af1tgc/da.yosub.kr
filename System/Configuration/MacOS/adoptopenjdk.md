---
title: Install adoptopenjdk 11 with homebrew
description: 
published: true
date: 2023-08-16T01:33:52.660Z
tags: system, jdk, java
editor: markdown
dateCreated: 2023-03-31T05:51:51.468Z
---

# MacOS에 adoptopenjdk 11 설치하기

1. homebrew 업데이트
```shell
brew update
``` 

2. java 설치
```shell
brew install --cask adoptopenjdk # newest
brew install --cask adoptopenjdk11 # specific version
```

3. m1 mac
16->17로 올라가면서 뭔가 바뀌었다...
```shell
brew tap homebrew/cask-versions
brew install --cask temurin17
```