---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/ablation-study-for-3-d-reconstruction/","tags":["Project","Project/Stereo2PCD"],"noteIcon":"","created":"2024-07-09, 01:47"}
---

# Overview
---
### Background
- 이전까지는 스테레오 카메라의 Baseline 길이를 20cm로 고정하고 실험을 진행하였으나, 어느정도 ==경향성==만 보일 뿐 물체를 판별할 수 정도의 정확성이 없었음

<br/>

### Purpose
- 좀 더 다양한 결과를 확인하기 위해 Baseline을 10cm, 20cm로 설정하고 물체까지의 거리를 1m, 2m, 3m로 설정하여 각각의 결과를 비교
- 위 실험의 결과를 바탕으로 최적의 Baseline을 구하고, 물체를 판별할 수 있는 가시 거리를 구함

<br/>

### Key Objectives
1. Baseline 10cm, 20cm에서 [[0_Project/00_Research Internship/001_3D Reconstruction/Stereo Calibration\|Stereo Calibration]]수행
2. 1m, 2m, 3m 거리의 물체를 촬영하고, [[0_Project/00_Research Internship/001_3D Reconstruction/3D Reconstruction from Stereo Images\|3D Reconstruction from Stereo Images]]을 수행하여 결과 비교
3. [[0_Project/00_Research Internship/001_3D Reconstruction/Extract PCD from Stereo Images (OpenCV)#cv2.StereoSGBM_create 파라미터\|cv2.StereoSGBM_create]]의 파라미터를 수정하여 최적의 값 찾기

<br/><br/>

# Progress
---
## Baseline - 20cm
### Calibration Parameters
```
Intrinsic Matrix 1:
[[2.63942735e+03 0.00000000e+00 2.79021597e+03]
 [0.00000000e+00 2.62601903e+03 2.47344923e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 1: 
[[ 0.03927038 -0.19292684  0.00514628  0.00021947  0.13714445]]

Intrinsic Matrix 2: 
[[2.63391078e+03 0.00000000e+00 2.83883135e+03]
 [0.00000000e+00 2.62538788e+03 2.36465065e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 2: 
[[ 0.03379473 -0.20853764 -0.00924497  0.00289502  0.24443901]]

Rotation Matrix: 
[[ 9.98923323e-01 -4.63902195e-02  3.78157609e-04]
 [ 4.63885769e-02  9.98726081e-01 -1.98573545e-02]
 [ 5.43511169e-04  1.98535168e-02  9.99802752e-01]]

Translation Matrix: 
[[-19.73456501]
 [ -0.72649425]
 [ -0.13871087]]
```

<br/>

### Results of 3D Reconstruction

- 1m
![3_Archive/31_Attachments/000000.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_imgL.jpg)![3_Archive/31_Attachments/000000.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000000.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000000.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>


![3_Archive/31_Attachments/제목 없는 동영상.gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81.gif)

<br/>

- 2m

![3_Archive/31_Attachments/000001.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL.jpg)![3_Archive/31_Attachments/000001.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000001.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000001.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>

![3_Archive/31_Attachments/제목 없는 동영상 (1).gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(1).gif)
<br/>

- 3m

![3_Archive/31_Attachments/000002.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL.jpg)![3_Archive/31_Attachments/000002.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000002.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000002.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>

![3_Archive/31_Attachments/제목 없는 동영상 (2).gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(2).gif)

<br/>

- 3m - undistortion 과정 제외

![3_Archive/31_Attachments/000002_2.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL.jpg)![3_Archive/31_Attachments/000002_2.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000002_2.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000002_2.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>

![3_Archive/31_Attachments/제목 없는 동영상 1.gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%201.gif)

<br/><br/>

## Baseline - 10cm
### Calibration Parameters
```
Intrinsic Matrix 1:
[[2.63757152e+03 0.00000000e+00 2.78345268e+03]
 [0.00000000e+00 2.62562066e+03 2.43905553e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 1: 
[[-0.00358519 -0.04612936  0.0018598  -0.00040883  0.05050566]]

Intrinsic Matrix 2: 
[[2.62548761e+03 0.00000000e+00 2.82446695e+03]
 [0.00000000e+00 2.61852950e+03 2.37269874e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 2: 
[[ 0.01194264 -0.06365393 -0.00700615  0.00145909  0.04981359]]

Rotation Matrix: 
[[ 0.99933046 -0.03567012 -0.00814124]
 [ 0.03572819  0.99933631  0.00710229]
 [ 0.0078825  -0.00738841  0.99994164]]

Translation Matrix: 
[[-9.85283962]
 [-0.20400332]
 [-0.0854086 ]]
```

<br/>

### Results of 3D Reconstruction

- 1m

![3_Archive/31_Attachments/000003.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_imgL.jpg)![3_Archive/31_Attachments/000003.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>
<br/>

![3_Archive/31_Attachments/000003.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000003.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>


![3_Archive/31_Attachments/제목 없는 동영상 (1) 1.gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(1)%201.gif)

<br/>

- 2m

![3_Archive/31_Attachments/000004.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL.jpg)![3_Archive/31_Attachments/000004.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000004.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000004.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>

![3_Archive/31_Attachments/제목 없는 동영상 (2) 1.gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(2)%201.gif)

<br/>

- 3m
![3_Archive/31_Attachments/000005.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL.jpg)![3_Archive/31_Attachments/000005.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000005.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000005.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>


![3_Archive/31_Attachments/제목 없는 동영상 (3).gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(3).gif)

<br/><br/>

### Discussion
- **Baseline - 20cm**
	- Disparity가 크기 때문에 먼 거리의 물체를 잘 포착한다는 장점이 있지만, 반대로 가까울수록 잘 포착하지 못하는 듯한 결과 보임
	- 3m 부터는 물체에 한해선 포착을 하지만, 빛이 조금이라도 강하던가 흰 색의 경우 거리를 제대로 계산하지 못함
		- 위 문제를 명확하게 하기 위해 한쪽 조명을 끄고 동일한 조건(3m)하에 진행해보았으나, 사진이 어두워 픽셀 간 차이가 적어서 그런지 거리를 거의 계산하지 못함

![3_Archive/31_Attachments/000005.JPG_imgL 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL%201.jpg)![3_Archive/31_Attachments/000005.JPG_imgL_undist 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_undist%201.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center><br/>

![3_Archive/31_Attachments/000005.JPG_imgL_rect 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_rect%201.jpg)![3_Archive/31_Attachments/000005.JPG_disparity 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_disparity%201.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center><br/>

![3_Archive/31_Attachments/제목 없는 동영상 (4).gif](/img/user/3_Archive/31_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(4).gif)

<br/>

- **Baseline - 10cm**
	- 1m 이내의 작은 물체의 경우 꽤 잘 포착하였으나, 그 이상의 경우에는 아예 이상한 결과가 나옴 

<br/><br/>

## cv2.StreoSGBM_create
[[0_Project/00_Research Internship/001_3D Reconstruction/Extract PCD from Stereo Images (OpenCV)\|StereoSGBM_create]]


[[3_Archive/32_Daily Notes/2024-07-11\|2024-07-11]]
# Resource
---

