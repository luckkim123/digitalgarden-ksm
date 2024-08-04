---
{"dg-publish":true,"permalink":"/1-area/11-study/115-sensors/stereo-camera/stereo-camera-depth-estimation/","tags":["Study/Camera/3D-Reconstruction","Project/Stereo2PCD"],"noteIcon":"","created":"2024-08-04"}
---

# Stereo Vision

- 사람의 시각 시스템을 모방한 기술
	- 사람은 두 눈으로부터 ==좌우 차이가 존재하는 2차원의 영상==을 입력받고, 입력 받은 영상을 인간의 뇌로부터 융합되는 과정을 통해 3차원의 거리 감을 인지
	- Stereo vision은 카메라를 통해 입력되는 ==2차원의 좌우 영상을 계산하면서 3차원의 거리 정보 획득==

<br/>

## Depth Estimation
- 3차원 거리 정보는 시차([[3_Archive/30_Fleeting Notes/Disparity Map (작성중)\|Disparity]]), 초점 거리(Focal length), 베이스라인(Baseline) 3가지 요소를 고려하여 얻을 수 있음
	- Disparity: Depth estimation을 위한 두 이미지에서 객체의 위치(x축) 상의 차이
	- Focal length: 이미지 평면(CCD, CMOS 센서)와 카메라 렌즈 사이의 거리
	- Baseline: 좌우 카메라의 간격

<br/>

>[!info|left-medium] 
>![3_Archive/31_Attachments/Pasted image 20240804161958.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240804161958.png)
><center style="font-size: 12; opacity: 0.7">Disparity 계산</center>

<br/><br/>

$$\begin{aligned}
z:b&=z-f:b-x_l+x_r\\\\
b\cdot z-b\cdot f&=b\cdot z-(x_r-x_l)\cdot z\\\\
z&=\frac{b\cdot f}{z_r-z_l}=\frac{b\cdot f}{d}
\end{aligned}$$


<br/><br/><br/><br/><br/><br/><br/><br/>

## Process of 3D Reconstruction

![3_Archive/31_Attachments/Pasted image 20240804164104.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240804164104.png)
