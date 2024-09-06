---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/stereo-calibration/","tags":["Project","Project/Stereo2PCD","Study/Camera/Calibration"],"noteIcon":"","created":"2024-07-09"}
---

- [Evernote](https://www.evernote.com/shard/s515/sh/3f586871-a7a9-d195-943c-f2b6f0aa830c/Bk850BxaddK85K-Q27CGX3xInL4AYbuC7i6nuUKX5K7vTG3Grh98G32IUg)
# Overview
---
### Purpose
- [[0_Project/00_Research Internship/001_3D Reconstruction/3D Reconstruction from Stereo Images\|3D Reconstruction from Stereo Images]] 를 수행하기 위해 좌우 GoPro 카메라의 Calibration 수행


### Background
- 기존에는 스테레오 비전 영상으로부터 포인트 클라우드 데이터를 생성 과제를 Calibration 없이 진행하려 하였으나, ==두 이미지 사이의 매칭 정보와 거리 정보 등을 알 수 없기 때문에== 포인트들이 제대로 생성되지 않는 문제 발생 
- 또한, GoPro11 의 경우 ==Auto focusing 기능==을 끄는 방법을 찾을 수 없기 때문에 해당 기능이 켜져있는지 확인 필요


### Key Objectives
1. 단일 카메라에서 데이터를 두 차례 취득한 뒤 Calibration 을 수행하여 Focal length 가 변하는지 확인
2. OpenCV 기반 Calibration tool 을 GoPro 데이터셋에 맞게 수정

<br/><br/>

# Progress
---
[[0_Project/00_Research Internship/001_3D Reconstruction/Kanban - 3D Reconstruction from Stereo Images\|진행 상황]]

- Ubuntu, OpenCV, Python 등의 호환성을 고려하여 ==Docker 로 진행==
	```bash
	docker run -it --privileged --gpus 'all,"capabilities=compute,utility,graphics"' -e DISPLAY=unix$DISPLAY -e QT_X11_NO_MITSHM=1 -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v /etc/localtime:/etc/localtime:ro -e TZ=Asia/Seoul -v /dev:/dev -v ~/workspace/dataset:/workspace/dataset -w /workspace --restart always --name stereo2pcd python:3.10.14-bullseye
	```

	- 참고 자료
		- [[2_Resource/1_Study/1_Coding/ETCs/VSCode 가상환경 코드 디버깅 수행\|VSCode 가상환경 코드 디버깅 수행]]
		- [[2_Resource/1_Study/1_Coding/ErrorFix/Open3D WARNING - GLFW Error\|Open3D WARNING - GLFW Error]]


## Stereo Calibration

1. ==체커보드 패턴으로 실세계 좌표 정의==
	- 세계 좌표는 체커보드 패턴으로 고정되며, 3D 점은 체커보드에 있는 사각형의 코너
	- $X$ 축과 $Y$ 축은 체커보드를 따라 있으며, $Z$ 축은 벽에 수직이기 때문에 $Z_w=0$
	- 캘리브레이션 과정에서, 알고 있는 3D  ($X_w, Y_w, Z_w$)과 해당 점과 대응되는 픽셀의 위치($u, v$)의 세트로 카메라 파라미터를 계산


1. ==다양한 시점에서 체커보드의 여러 이미지 캡쳐==
	- 체커보드를 정적으로 유지하고 카메라를 움직여 체커보드의 여러 이미지를 찍거나, 카메라를 일정하게 유지하고 다른 방향에서 체커보드 패턴을 촬영


1. 체커보드의 2D 좌표 찾기 - `cv2.findChessboardCorners`
	```python
	retval, corners = cv2.findChessboardCorners(image, patternSize, flags)
	```
	- Parameters
		- **image**: 소스 체커보드 사진. 8-bit 그레이스케일 또는 컬러 이미지
		- **patternSize**: 체커보드 행과 열당 내부 코너 수
		- **corners**: 감지된 코너의 출력 배열
		- **flags**: 다양한 작업 플래그


1. ==카메라 캘리브레이션== - `cv2.calibrateCamera`
	- 세계 좌표의 3D 점과 모든 이미지의 2D 위치를 OpenCV의 calibrateCamera방법으로 전달
	```python
	retval, cameraMatrix, distCoeffs, rvecs, tvecs = cv2.calibrateCamera(objectPoints, imagePoints, imageSize)
	```
	- Parameters
		- **objectPoints**: 3D 점 벡터로 구성된 벡터. 외부 벡터는 패턴 사진의 수만큼 요소를 포함
		- **imagePoints**: 2D 이미지 점 벡터로 구성된 벡터
		- **imageSize**: 이미지의 크기
		- **cameraMatrix**: 내부 카메라 행렬
		- **distCoeffs**: 렌즈 왜곡 계수(Lens distortion coefficients)
		- **rvecs**: 회전은 3×1 벡터로 지정. 벡터의 방향은 회전 축을 지정하고 벡터의 크기는 회전 각을 지정
		- **tvecs**: 3×1 이동 벡터

	![3_Archive/1_Attachments/Pasted image 20240709175326.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709175326.png)
	$\text{Distortion coefficients} = (k_1 k_2 p_1 p_2 k_3)$


1. 스테레오 카메라 캘리브레이션 - `cv2.stereoCalibrate`
	- 두 대의 카메라를 사용하여 스테레오 비전을 구현하기 위한 캘리브레이션을 수행
	- 두 카메라의 내·외부 파라미터를 계산하여, 두 카메라의 좌표계를 일치시킴
	
	```python
	retval, cameraMatrix1, distCoeffs1, cameraMatrix2, distCoeffs2, R, T, E, F = cv2.stereoCalibrate(objectPoints, imagePoints1, imagePoints2, cameraMatrix1, distCoeffs1, cameraMatrix2, distCoeffs2, imageSize, R=None, T=None, E=None, F=None, criteria=None, flags=None)
	```

	- Parameters
		- **objectPoints**: 3D 공간의 각 코너 점 좌표. (리스트 형태로 N개의 3D 포인트)
		- **imagePoints1**: 첫 번째 카메라에서의 이미지 좌표. (리스트 형태로 N개의 2D 포인트)
		- **imagePoints2**: 두 번째 카메라에서의 이미지 좌표. (리스트 형태로 N개의 2D 포인트)
		- **cameraMatrix1**: 첫 번째 카메라의 내파라미터 행렬. (3x3 행렬)
		- **distCoeffs1**: 첫 번째 카메라의 왜곡 계수. (5x1 또는 8x1 행렬)
		- **cameraMatrix2**: 두 번째 카메라의 내파라미터 행렬. (3x3 행렬)
		- **distCoeffs2**: 두 번째 카메라의 왜곡 계수. (5x1 또는 8x1 행렬)
		- **imageSize**: 이미지 크기 (width, height)
		- **R**: 두 카메라 간의 회전 행렬. (3x3 행렬)
		- **T**: 두 카메라 간의 이동 벡터. (3x1 벡터)
		- **E**: 필수 행렬. (3x3 행렬)
		- **F**: 기본 행렬. (3x3 행렬)
		- **criteria**: 최적화 반복 종료 기준. (cv2.TERM_CRITERIA 타입)
		- **flags**: 특정 옵션을 지정하는 플래그. (cv2.CALIB 타입)


### Issues - Distortion Coeifficient

- OpenCV tool 로 구한 왜곡 계수(Distortion coeifficient)를 사용하여 cv2.undistortion 을 한 결과 원본 사진보다 왜곡된 듯한 결과가 보임


#### Solutions

- Matlab 의 Stereo camera calibration tool 로 구한 왜곡 계수와 비교해본 결과 차이가 있었으며, 어떤 계수가 정확한 것인지 확인하기 위해 3D reconstruction 까지 수행하여 결과 비교

|  0.00201   |  -0.01563   |     0      |      0      |     0      |
| :--------: | :---------: | :--------: | :---------: | :--------: |
|            |             |            |             |            |
| **0.0332** | **-0.1465** | **0.0020** | **-0.0003** | **0.1641** |
<center style="font-size: 12; opacity: 0.7">Matlab 에서 구한 Dist coeff (위) / OpenCV 에서 구한 Dist coeff (밑)</center>

![3_Archive/1_Attachments/Pasted image 20240709195741.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709195741.png)![3_Archive/1_Attachments/Pasted image 20240709195756.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709195756.png)
<center style="font-size: 12; opacity: 0.7">Matlab 에서 구한 Dist coeff (좌) / OpenCV 에서 구한 Dist coeff (우)</center>

<br/><br/>
# Resource
---

- [opencv/samples/python/stereo\_...](https://github.com/opencv/opencv/blob/master/samples/python/stereo_match.py)
- [OpenCV 07-4. Depth Map fro...](https://leechamin.tistory.com/362)
- [2장의 이미지로 3차원 복원하기 with Python ...](https://zzziito.tistory.com/45)
- [OpenCV Camera Calibration(카...](https://moon-coco.tistory.com/entry/OpenCVCamera-Calibration%EC%B9%B4%EB%A9%94%EB%9D%BC-%EC%99%9C%EA%B3%A1-%ED%8E%B4%EA%B8%B0)
- [OpenCV: 카메라 캘리브레이션(Camera Cali...](https://foss4g.tistory.com/1665)
