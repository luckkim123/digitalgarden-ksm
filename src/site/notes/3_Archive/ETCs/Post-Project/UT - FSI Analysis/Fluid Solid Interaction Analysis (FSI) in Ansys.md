---
{"dg-publish":true,"permalink":"/3-archive/et-cs/post-project/ut-fsi-analysis/fluid-solid-interaction-analysis-fsi-in-ansys/","tags":["Project"],"noteIcon":"","created":"2024-09-08"}
---

# Overview
### Background
- Cyclops가 수중에서 움직일 때, 부착된 HERO wings에 걸리는 응력을 분석하고, 이를 바탕으로 Cyclops의 속력과 HERO wings의 각도에 따른 파손의 상관관계 파악


<br/>

### Purpose
- Ansys 소프트웨어를 사용하여 유체-구조 연성 해석(Fluid-Solid Interaction, FSI)를 수행
- HERO wings에 가해지는 응력과 변형을 분석하여 Cyclops의 속도 및 Wings의 각도에 따른 최대 응력을 계산
- 계산된 응력을 재료의 피로 한도(SN curve)와 비교하여 Cyclops의 안전한 운전 조건 설정


<br/>

### Key Objectives
- Ansys에 HERO wings의 3D 모델을 정확하게 가져와 FSI 해석 진행
- Cyclops의 속도와 HERO wings의 각도에 따른 최대 응력 값 도출
- 최대 응력 값을 SN curve와 비교하여 Cyclops의 안전한 속도 및 Wings의 각도 범위 설정


<br/><br/>

# Progress
### Issues - 3D Modeling 문제
- HERO wings의 3D 모델이 `.dae` 포맷으로 제공되었으나, Ansys에서 지원되지 않아 `.stl`로 변환해야함
- 메쉬 결함으로 인해 FSI 해석이 제대로 이루어지지 않았으며, 정확한 응력 및 변형 분석에 문제가 발생생

![3_Archive/1_Attachments/Pasted image 20240908202934.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908202934.png)
![3_Archive/1_Attachments/Pasted image 20240908203045.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908203045.png)

<br/>

#### Root Cause Analysis
- 포맷 변환을 제공하는 사이트를 통해 `.stl` 포맷으로 변환하였으나, 이 과정에서 메쉬 정보가 손실되었고, Ansys로 가져왔을 때 구멍이 발생

![3_Archive/1_Attachments/HERO_Wings_v1 v2.png](/img/user/3_Archive/1_Attachments/HERO_Wings_v1%20v2.png)![3_Archive/1_Attachments/HERO_Wings_Links v3.png](/img/user/3_Archive/1_Attachments/HERO_Wings_Links%20v3.png)

<br>

#### Solutions
- Autodesk의 Fusion 360 소프트웨어를 사용하여 HERO wings의 3D 모델을 다시 설계
	- 직접 측정한 치수를 기준으로 모델링을 하여 Ansys에서 요구하는 메쉬 품질을 충족시켰으며, 이후 FSI 해석을 위한 메쉬 설정을 조정함

![3_Archive/1_Attachments/Pasted image 20240908203346.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908203346.png)

<br>

### Issues - Two-way FSI 해석 시 Data Transfer에서 문제 발생
- Two-way FSI 해석에서 Fluent와 Static Structural 간 데이터 전송에서 오류가 발생하여 해석이 진행되지 않음
- One-way FSI에서는 큰 문제가 없었으나, 두 해석 모듈이 상호 데이터를 주고 받는 과정에서 에러가 발생
- Two-way FSI는 실제 유체와 구조의 상호작용을 정확하게 모사하므로, 이 해석이 불가능하면 실제 파손 조건을 예측하기 어짐

![3_Archive/1_Attachments/Pasted image 20240908203840.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908203840.png)![3_Archive/1_Attachments/Pasted image 20240908204142.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908204142.png)

![3_Archive/1_Attachments/Pasted image 20240908204133.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908204133.png)![3_Archive/1_Attachments/Pasted image 20240908204121.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240908204121.png)

<br/>

#### Root Cause Analysis
- Fluent에서 계산된 유체 데이터가 Static structural로 제대로 전달되지 않거나, 두 해석 간의 상호 데이터 전송 오류가 발생
- 두 모듈 간 데이터 형식 및 시간적 매칭 문제가 발생했을 가능성이큼

<br>

#### Solutions
- Two-way FSI가 불가능하므로, Cyclops의 속도와 HERO wings 각도에 따른 여러 시나리오 테스트를 진행
- 재료의 SN curve를 인터넷에서 구해, 계산된 최대 응력과 비교하며 HERO wings의 안전한 운전 범위 결정


![3_Archive/1_Attachments/2024-09-08204617-ezgif.com-video-to-gif-converter.gif](/img/user/3_Archive/1_Attachments/2024-09-08204617-ezgif.com-video-to-gif-converter.gif)
![3_Archive/1_Attachments/2024-09-08204658-ezgif.com-video-to-gif-converter.gif](/img/user/3_Archive/1_Attachments/2024-09-08204658-ezgif.com-video-to-gif-converter.gif)

|                  | Minimum  | Maximum | Average |
| :--------------- | :------- | :------ | :------ |
| Stress [Mpa]     | 1.272e-5 | 958.4   | 41.40   |
| Deformation [mm] | 0.       | 40.65   | 15.66   |


<br/><br/>

# Resource
- [[2_Resource/1_Study/ETCs/Ansys/Fluid Solid Interaction Analysis (FSI)\|Fluid Solid Interaction Analysis (FSI)]]
- [[2_Resource/1_Study/ETCs/Ansys/Two-Way FSI in Ansys\|Two-Way FSI in Ansys]]
