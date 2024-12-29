---
{"dg-publish":true,"permalink":"/0-project/3-d-reconstruction/3-d-reconstruction-from-stereo-images/","tags":["Project","Project/Stereo2PCD","Study/Camera/Calibration","Study/Camera/3D-Reconstruction"],"noteIcon":"","created":"2024-07-09"}
---

- [Evernote](https://www.evernote.com/shard/s515/sh/a1ebdaac-9a64-3b3b-e770-b1543c9a5f6b/qIz3RpnuFc5hSHTRQYZcixyTk6e7nKCVKzhXDEYUbAXuje1fesA0VE1lCw)
# Overview
### Purpose
- ==스테레오 카메라 이미지를 통해 포인트 클라우드 데이터(PCD)를 생성==하는 방법을 연구하고, 이를 해양 환경에서 소나(Sonar) 센서와 함께 사용할 수 있도록 연구


### Background
- 소나 센서는 거리 정보를 비교적 정확하게 얻을 수 있으나, 물체의 높이(Elevation) 및 맥락(Contextual) 정보가 부족함
- 반면에, 카메라는 물체의 맥락 정보를 풍부하게 제공할 수 있으나, 감지 거리가 짧고 거리 정보를 제공하지 못하는 단점 존재
- 따라서, 이 연구는 ==스테레오 카메라를 사용하여 PCD를 추출하고, 이를 소나 센서와 융합==하여 두 센서의 장점을 극대화하고, 단점을 보완하는 것을 목표로 함


### Key Objectives
1. 좌우 비전 영상의 시간 동기화
2. 스테레오 비전 영상으로부터 PCD 생성
    - 초기에는 캘리브레이션 없이 진행하며, PCD 생성이 어려운 경우 캘리브레이션을 수행하거나 추가 데이터를 사용하여 진행

<br/><br/>
# Progress

[[0_Project/3D Reconstruction/Kanban - 3D Reconstruction from Stereo Images\|진행 현황]]
<br/>
## Undistortion
- 왜곡된 이미지에서 렌즈 왜곡을 제거하는 과정
- 왜곡 계수와 카메라 행렬을 사용하여 왜곡된 이미지에서 새로운 카메라 행렬을 통해 왜곡을 제거한 이미지를 얻음

```python
def undistort(frame, K, dist):
    h, w = frame.shape
    newCameraMat, roi = cv2.getOptimalNewCameraMatrix(K, dist, (w, h), 1)
    undistortedImg = cv2.undistort(frame, K, dist, None)
    return undistortedImg
```

- `cv2.getOptimalNewCameraMatrix`: 왜곡을 제거한 후의 새로운 카메라 행렬을 계산.
- `cv2.undistort`: 주어진 카메라 행렬과 왜곡 계수를 사용하여 이미지를 왜곡 제거.


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/0-project/3-d-reconstruction/stereo-calibration/#issues-distortion-coeifficient" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



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

</div></div>


## Rectification
- 두 카메라 이미지의 에피폴라 기하학을 정렬하는 과정
- 두 이미지의 스캔 라인이 동일 평면에 위치하게 만들어, 스테레오 매칭을 쉽게 만듬

```python
def rectify(imgL_undist, imgR_undist, K1, dist1, K2, dist2, R, T):
    h, w = imgL_undist.shape
    R1, R2, P1, P2, _, _, _ = cv2.stereoRectify(K1, dist1, K2, dist2, (w, h), R, T)
    mapLx, mapLy = cv2.initUndistortRectifyMap(K1, dist1, R1, P1, (w, h), cv2.CV_32FC1)
    mapRx, mapRy = cv2.initUndistortRectifyMap(K2, dist2, R2, P2, (w, h), cv2.CV_32FC1)
    imgL_rect = cv2.remap(imgL_undist, mapLx, mapLy, cv2.INTER_LINEAR)
    imgR_rect = cv2.remap(imgR_undist, mapRx, mapRy, cv2.INTER_LINEAR)
    return imgL_rect, imgR_rect
```

- `cv2.stereoRectify`: 스테레오 정렬 행렬과 투영 행렬을 계산.
- `cv2.initUndistortRectifyMap`: 왜곡 및 정렬 맵을 계산.
- `cv2.remap`: 왜곡 및 정렬된 이미지를 생성.

![3_Archive/1_Attachments/Pasted image 20240709203045.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709203045.png)![3_Archive/1_Attachments/Pasted image 20240709203105.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709203105.png)
<center style="font-size: 12; opacity: 0.7">Matlab 에서 구한 Dist coeff (좌) / OpenCV 에서 구한 Dist coeff (우)</center>

<br/>

## Stereo Matching
- 좌우 이미지 간의 디스패리티 맵(disparity map)을 계산하여, 각 픽셀의 깊이를 추정하는 과정

```python
def matching(imgL_rect, imgR_rect):
    left_matcher = cv2.StereoSGBM_create(minDisparity=0, numDisparities=16*80, blockSize=11,
                                         uniquenessRatio=1, speckleWindowSize=150, speckleRange=2,
                                         disp12MaxDiff=-1, P1=600, P2=2400)
    right_matcher = cv2.ximgproc.createRightMatcher(left_matcher)
    wls_filter = cv2.ximgproc.createDisparityWLSFilter(matcher_left=left_matcher)
    wls_filter.setLambda(8e4)
    wls_filter.setSigmaColor(1.2)
    
    dispL = left_matcher.compute(imgL_rect, imgR_rect)
    dispR = right_matcher.compute(imgR_rect, imgL_rect)
    disp = wls_filter.filter(dispL, imgL_rect, None, dispR)
    disp = cv2.normalize(disp, disp, 0, 255, cv2.NORM_MINMAX)
    disp = np.uint8(disp)
    return disp
```

- `cv2.StereoSGBM_create`: 스테레오 매칭 알고리즘([[2_Resource/1_Study/1_Coding/OpenCV/stereoSGBM_create\|Stereo SGBM]]) 생성. 
- `cv2.ximgproc.createRightMatcher`: 오른쪽 매칭 생성.
- `cv2.ximgproc.createDisparityWLSFilter`: 좌우 디스패리티를 조화롭게 필터링.
- `cv2.normalize`: 결과 디스패리티 맵을 정규화.

![3_Archive/1_Attachments/Pasted image 20240709203224.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709203224.png)![3_Archive/1_Attachments/Pasted image 20240709203232.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240709203232.png)
<center style="font-size: 12; opacity: 0.7">Matlab 에서 구한 Dist coeff (좌) / OpenCV 에서 구한 Dist coeff (우)</center>
<br/>

## Reconstruction
- 디스패리티 맵에서 3D 포인트 클라우드를 추출하는 과정
- 각 픽셀의 깊이를 이용하여 3D 공간의 좌표를 계산

```python
def extract(imgL, disp, K1, K2, T, PLY_SAVE):
    cx = K1[0, 2]
    cy = K1[1, 2]
    cx_ = K2[0, 2]
    fx = K1[0, 0]
    Tx = T[0, 0]
	# _, _, _, _, Q, _, _ = cv2.stereoRectify(K1, dist1, K2, dist2, (w, h), R, T)
    Q = np.float32([[1, 0, 0, -cx],
                    [0, 1, 0, -cy],
                    [0, 0, 0, fx],
                    [0, 0, -1/Tx, (cx - cx_)/Tx]])
    
    points = cv2.reprojectImageTo3D(disp, Q)
    colors = cv2.cvtColor(imgL, cv2.COLOR_BGR2RGB)
    
    mask = disp > disp.min()
    points = points[mask]
    colors = colors[mask]
    
    write_ply(PLY_SAVE, points, colors)
```

<br/>

### Issues - Q matrix
- OpenCV 에서는 Reconstruction 을 하기 위해 `cv2.reprojectImageTo3D` 함수를 사용하며, `disparity map` 과 `Q` 행렬이 인자로 들어감
- 이때, `Q` 행렬은 `cv2.stereoRectify` 함수에서 계산되는데 계산 식은 다음과 같음
  ![3_Archive/1_Attachments/Pasted image 20240705171519.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240705171519.png)
- 하지만 `cv2.stereoRectify` 에서 구해진 결과 값과 수동으로 계산한 값이 차이가 있음

|  1  |  0  |    0    | -2776.3 |
| :-: | :-: | :-----: | ------- |
|  0  |  1  |    0    | -2444.0 |
|  0  |  0  |    0    | 2658.0  |
|  0  |  0  | -0.041  | -0.0830 |
|     |     |         |         |
|  1  |  0  |    0    | -2770.0 |
|  0  |  1  |    0    | -2435.2 |
|  0  |  0  |    0    | 2642.1  |
|  0  |  0  | -0.0405 | **0**   |
<center style="font-size: 12; opacity: 0.7">cv2.stereoRectify 에서 구한 Q matrix (위) / 수동으로 구한 Q matrix (밑)</center>

![[3_Archive/1_Attachments/test3-3-2024-07-05_15.24.54.mp4]]
<center style="font-size: 12; opacity: 0.7">cv2.stereoRectify 에서 구한 Q matrix 의 Reconstruction 결과 값</center>

![[3_Archive/1_Attachments/test3-4-2024-07-05_15.37.11.mp4]]
<center style="font-size: 12; opacity: 0.7">수동으로 구한 Q matrix 의 Reconstruction 결과 값</center>

# Resource


