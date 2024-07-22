---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/video-ray/","tags":["Project","gardenEntry","gardenEntry"],"dgShowLocalGraph":true,"dgShowFileTree":true,"dgEnableSearch":true,"dgShowToc":true}
---

# Overview
---
### Background
![3_Archive/31_Attachments/Pasted image 20240711164750.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711164750.png)![3_Archive/31_Attachments/Pasted image 20240711164803.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711164803.png)
<center style="font-size: 12; opacity: 0.7">VideoRay 로봇 (좌) / 무게 추 (우)</center>

- 8월 달 로봇 박람회에서 시연을 하는 로봇에 무게 추를 고정하는 부분이 고장이 났기 때문에 수리하기로 하였음

<br/>

### Purpose
- 기존에는 아크릴 판으로 무게 추와 로봇을 고정하였는데, 해당 아크릴 판이 부서졌기 때문에 해당 부분을 수리
- 박람회 시연 중, 해당 로봇에 자석을 부착하고 자석이 부착된 여러 물건을 준비하여 아이들이 로봇을 조종하여 물체를 집을 수 있게 하기로 함

<br/>

### Key Objectives
- ==기존에는 5mm 아크릴 판에 M3 볼트로 로봇과 고정==하였는데 ==결국 1mm 부분만 무게 추를 지지==하였기 때문에 아크릴 판이 부서짐
	- 볼트가 지지대에 가하는 힘을 최대한 분산하여 오래 버틸 수 있도록 함
- 지지대 부분에 자석을 고정시킬 수 있는 부분 추가가

<br/><br/>

# Progress
---
![3_Archive/31_Attachments/Pasted image 20240711170800.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711170800.png)

## 로봇 결합
![3_Archive/31_Attachments/Pasted image 20240711172338.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711172338.png)![3_Archive/31_Attachments/Pasted image 20240711171236.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711171236.png)

- 로봇과 결합하기 위해 너트와 볼트를 넣어 결합할 수 있는 공간 설계
	- 볼트는 M3 X20 크기를 선택하였음

<br/>

### Issues - 지지대 안정성
- 사진에서 보이는 바와 같이 볼트 구멍과 로봇과의 거리가 매우 짧으며(약 5mm), 구멍이 M4 크기이기 때문에 지지대를 최대한 두껍게 만들어도 M4 볼트를 사용하면 2mm 두께의 필라멘트 만으로 무게 추를 지지해야함

<br/>

#### Solutions
- M3 볼트를 선택하고, 구멍의 위치를 M4 크기 구멍 제일 바깥쪽에 위치하게 하여, 결과적으로 3mm 두께의 필라멘트로 지지하도록 하였으며, 20mm 길이의 볼트를 선택하여 지지 면적을 넓힘

<br/><br/>

## 무게 추 및 자석 고정
![3_Archive/31_Attachments/Pasted image 20240711172521.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711172521.png)

- 무게 추와 자석을 고정할 수 있는 부품을 추가하였으며, M4 볼트로 체결할 수 있게 설계

<br/><br/>

## 3D model을 3D Printer로 출력하기
1. 3D modeling tool에서 모델링 파일을 `stl` 확장자로 내보니기
	![3_Archive/31_Attachments/Pasted image 20240711182334.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711182334.png)![3_Archive/31_Attachments/Pasted image 20240711182347.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711182347.png)


1. 사용 중인 3D printer의 소프트웨어를 다운로드 받은 후, `GCODE` 파일로 내보내기
	![3_Archive/31_Attachments/Pasted image 20240711182908.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240711182908.png)
2. `GCODE` 파일을 USB에 옮겨 담은 후, 3D printer에 파일을 로드하고 실행
	- 주의사항: 오토레벨링이 실패할 경우 프린터기가 동작하지 않기 때문에, 항상 확인하고 퇴근할 것
		- 오토레벨링 (Auto Leveling)
		  3D 프린터기가 물체가 잘 출력되도록 팔레트의 수평을 맞추는 작업

# Resource
---
