---
{"dg-publish":true,"permalink":"/2-resource/1-study/1-coding/docker/window-docker-docker/","tags":["#Study/Coding/Docker"],"noteIcon":"","created":"2024-07-31"}
---

>[!note] 목차
>1. ~~[[2_Resource/1_Study/1_Coding/Docker/Window에서 Docker 사용하기 - WSL2 설치\|WSL2 설치]]~~
>2. **Docker 설치**
>3. [[2_Resource/1_Study/1_Coding/Docker/Window에서 Docker 사용하기 - IDE 연결\|IDE 연결]]

# Docker 설치

1. **Docker for Windows** 설치
	[Docker 설치 링크](https://www.docker.com/)
	![3_Archive/1_Attachments/Pasted image 20240731145240.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731145240.png)![3_Archive/1_Attachments/Pasted image 20240731145251.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731145251.png)
2. Docker 확인하기
	```shell
	sudo docker run --rm --gpus all nvidia/cuda:11.0.3-base-ubuntu20.04 nvidia-smi
	```
	![3_Archive/1_Attachments/Pasted image 20240731155622.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731155622.png)