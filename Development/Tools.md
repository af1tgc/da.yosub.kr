---
title: FFMPEG
description: 
published: true
date: 2023-08-01T12:23:48.889Z
tags: 
editor: markdown
dateCreated: 2023-08-01T12:23:48.889Z
---

# FFMPEG Command
## split video to image
```bat
ffmpeg -ss 00:00:0 -i test.mp4 -r 10 -f image2 test-%d.jpg
```