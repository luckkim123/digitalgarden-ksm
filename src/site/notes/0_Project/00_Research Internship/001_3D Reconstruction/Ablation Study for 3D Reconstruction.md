---
{"date":"2024-07-09, 01:47","status":"Project","tags":["Project","Project/Stereo2PCD"],"aliases":null,"keywords":null,"related notes":null,"reference":null,"author":null,"url":null,"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/ablation-study-for-3-d-reconstruction/","dgPassFrontmatter":true}
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
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000000.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000000.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000000.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>


![[3_Archive/31_Attachments/20-1-2024-07-10_16.02.22.mp4]]

- 2m

![3_Archive/31_Attachments/000001.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL.jpg)![3_Archive/31_Attachments/000001.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000001.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000001.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000001.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/20-2-2024-07-10_16.08.53.mp4]]

- 3m

![3_Archive/31_Attachments/000002.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL.jpg)![3_Archive/31_Attachments/000002.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000002.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000002.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000002.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/20-3-2024-07-10_16.12.07.mp4]]

- 3m - undistortion 과정 제외

![3_Archive/31_Attachments/000002_2.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL.jpg)![3_Archive/31_Attachments/000002_2.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000002_2.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000002_2.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000002_2.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/20-4-2024-07-10_16.56.58.mp4]]

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

![3_Archive/31_Attachments/000003.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000003.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000003.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/10-1-2024-07-10_15.37.02.mp4]]
- 2m

![3_Archive/31_Attachments/000004.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL.jpg)![3_Archive/31_Attachments/000004.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000004.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000004.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000004.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/10-2-2024-07-10_15.43.26.mp4]]

- 3m

![3_Archive/31_Attachments/000005.JPG_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL.jpg)![3_Archive/31_Attachments/000005.JPG_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_undist.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000005.JPG_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_rect.jpg)![3_Archive/31_Attachments/000005.JPG_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_disparity.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/10-3-2024-07-10_15.48.26.mp4]]

<br/><br/>

### Discussion
- **Baseline - 20cm**
	- Disparity가 크기 때문에 먼 거리의 물체를 잘 포착한다는 장점이 있지만, 반대로 가까울수록 잘 포착하지 못하는 듯한 결과 보임
	- 3m 부터는 물체에 한해선 포착을 하지만, 빛이 조금이라도 강하던가 흰 색의 경우 거리를 제대로 계산하지 못함
		- 위 문제를 명확하게 하기 위해 한쪽 조명을 끄고 동일한 조건(3m)하에 진행해보았으나, 사진이 어두워 픽셀 간 차이가 적어서 그런지 거리를 거의 계산하지 못함

![3_Archive/31_Attachments/000005.JPG_imgL 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL%201.jpg)![3_Archive/31_Attachments/000005.JPG_imgL_undist 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_undist%201.jpg)
<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>

![3_Archive/31_Attachments/000005.JPG_imgL_rect 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_imgL_rect%201.jpg)![3_Archive/31_Attachments/000005.JPG_disparity 1.jpg|+grid](/img/user/3_Archive/31_Attachments/000005.JPG_disparity%201.jpg)
<center style="font-size: 12; opacity: 0.7">Recrified / Disparity map</center>

![[3_Archive/31_Attachments/20-6-2024-07-10_16.42.59.mp4]]

<br/>

- **Baseline - 10cm**
	- 1m 이내의 작은 물체의 경우 꽤 잘 포착하였으나, 그 이상의 경우에는 아예 이상한 결과가 나옴 

<br/><br/>

## cv2.StreoSGBM_create
[[0_Project/00_Research Internship/001_3D Reconstruction/Extract PCD from Stereo Images (OpenCV)\|StereoSGBM_create]]


[[3_Archive/32_Daily Notes/2024-07-11\|2024-07-11]]
# Resource
---

