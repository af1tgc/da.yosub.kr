---
title: Too many levels of symbolic links
description: 
published: true
date: 2023-05-09T07:15:30.189Z
tags: configuration, linux, unix
editor: markdown
dateCreated: 2023-05-09T07:15:30.188Z
---

# "Too many levels of symbolic links" 에러 해결
바이너리 파일을 링크할때, $PATH에 바인딩하는 것이 아니라 해당 바이너리를 직접 링크 시켜 사용하는 경우가 있을 수 있다.
이 경우, 바이너리 디렉토리에 찾아가서 단일 파일로 링크를 시키면 다음 에러가 발생할 수 있다.

```
zsh: too many levels of symbolic links: {$CMD}
```

이 경우, Absolute Path 로 링크를 시켜주면 해결 가능하다.
```shell
sudo ln -s "$(pwd)/{$CMD}" /usr/local/bin/
```

Relative Path를 사용할 경우, 다음 옵션을 추가하면 해결된다고 한다. (추가 확인 필요)
```shell
sudo ln -sr {$CMD} /usr/local/bin/
```