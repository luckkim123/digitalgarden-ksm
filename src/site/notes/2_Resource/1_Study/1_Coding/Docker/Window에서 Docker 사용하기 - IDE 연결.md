---
{"dg-publish":true,"permalink":"/2-resource/1-study/1-coding/docker/window-docker-ide/","tags":["Study/Coding/Docker"],"noteIcon":"","created":"2024-07-31"}
---

>[!note] 목차
>1. ~~[[2_Resource/1_Study/1_Coding/Docker/Window에서 Docker 사용하기 - WSL2 설치\|WSL2 설치]]~~
>2. ~~[[2_Resource/1_Study/1_Coding/Docker/Window에서 Docker 사용하기 - Docker 설치\|Docker 설치]]~~
>3. **IDE 연결**

# IDE 연결
1. VScode 다운로드
	[vscode 설치 링크](https://code.visualstudio.com/docs/?dv=win)

1. VScode extension 설치
   Python, Docker, Docker explorer extension

1. WSL에서 Docker container를 실행하면 Docker desktop 왼쪽의 Container 탭과 VScode의 Docker extension에서 확인 가능
   ![3_Archive/1_Attachments/Pasted image 20240731154625.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731154625.png)
   ![3_Archive/1_Attachments/Pasted image 20240731154643.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731154643.png)![3_Archive/1_Attachments/Pasted image 20240731154847.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731154847.png)
2. Dev containers extension 설치
   - VScode의 왼쪽 Extension 탭에서 Remote explorer를 클릭하면 WSL targets에서 Ubuntu와 Dev containers에서 Docker container 목록을 확인 가능
   - 해당 Container 혹은 Ubuntu를 Connect 하면 VScode에서 터미널로 사용 가능
	![3_Archive/1_Attachments/Pasted image 20240731155359.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240731155359.png)
