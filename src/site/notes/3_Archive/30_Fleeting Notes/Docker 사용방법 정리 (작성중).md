---
date: 2024-08-13
status: Fleeting
tags: 
aliases: 
keywords: 
reference: 
author: 
url: 
dg-publish: true
---
# Docker란?
- 어쩌구 저쩌구

- Docker pull, search, run, save, load, Dockerfile 등 사용 방법 정리

- docker cp

## Docker Run Example

```shell
docker run -it --privileged --gpus 'all,"capabilities=compute,utility,graphics"' -e DISPLAY=unix$DISPLAY -e QT_X11_NO_MITSHM=1 -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v /etc/localtime:/etc/localtime:ro -e TZ=Asia/Seoul -v /dev:/dev -w /workspace -v ~/workspace/dataset:/workspace/dataset --name hello-world hello-world nvidia-smi
```