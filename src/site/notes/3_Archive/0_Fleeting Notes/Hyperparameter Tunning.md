---
{"dg-publish":true,"permalink":"/3-archive/0-fleeting-notes/hyperparameter-tunning/","tags":["Project/Stereo2PCD"],"noteIcon":"","created":"2024-08-05"}
---

- Calibration parameters
	```
	Intrinsic Matrix 1:
	[[2.61823793e+03 0.00000000e+00 2.75870357e+03]
	 [0.00000000e+00 2.62762659e+03 2.44155682e+03]
	 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]
	
	Distortion Coeifficient 1: 
	[[-0.01010289 -0.0113979  -0.00127904  0.00286359  0.00717239]]
	
	Intrinsic Matrix 2: 
	[[2.62369756e+03 0.00000000e+00 2.77941317e+03]
	 [0.00000000e+00 2.62157243e+03 2.44901503e+03]
	 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]
	
	Distortion Coeifficient 2: 
	[[ 0.0080066  -0.06596141  0.00045156  0.00280416  0.06071294]]
	
	Rotation Matrix: 
	[[ 0.99987906  0.01364484  0.00746196]
	 [-0.01350582  0.99973997 -0.0183735 ]
	 [-0.00771072  0.01827049  0.99980335]]
	
	Translation Matrix: 
	[[-20.16332411]
	 [  0.25729197]
	 [  0.27413047]]
	```

## Test 1
```python
PARAMS = {
    "minDisparity": 0,
    "numDisparities": 16 * 80,
    "blockSize": 11,
    "disp12MaxDiff": 1,
    "uniquenessRatio": 10,
    "speckleWindowSize": 100,
    "speckleRange": 2,
    "mode": cv2.STEREO_SGBM_MODE_SGBM_3WAY
}
PARAMS["P1"] = 8 * 3 * PARAMS["blockSize"] ** 2
PARAMS["P2"] = 32 * 3 * PARAMS["blockSize"] ** 2
```

- Original #mcl/list-card
  ![3_Archive/1_Attachments/1_imgL.jpg](/img/user/3_Archive/1_Attachments/1_imgL.jpg)
- Undistorted
  ![3_Archive/1_Attachments/1_imgL_undist.jpg](/img/user/3_Archive/1_Attachments/1_imgL_undist.jpg)
- Rectified
  ![3_Archive/1_Attachments/1_imgL_rect.jpg](/img/user/3_Archive/1_Attachments/1_imgL_rect.jpg)
- Disparity map
	![3_Archive/1_Attachments/1_disparity.jpg](/img/user/3_Archive/1_Attachments/1_disparity.jpg)


![3_Archive/1_Attachments/Animation.gif](/img/user/3_Archive/1_Attachments/Animation.gif)

### Discussion
- Undistortion을 보면 원본과 거의 바뀐 것이 없는데 원본에서 왜곡이 거의 없기 때문이라고 판단되며, 실제로는 조금 보정이 되었음
  ![3_Archive/1_Attachments/result_screenshot_05.08.2024.png|300](/img/user/3_Archive/1_Attachments/result_screenshot_05.08.2024.png)
- 당장 먼저 생각할 수 있는 것은 `minDisparity`와 `numDisparities`가 depth와 관련이 있고, `blockSize`는 얼마나 세밀한, 혹은 정확한 Matching을 할 수 있게 하므로, 이 파라미터들을 먼저 수정하는 것

<br/>

## Test 2
```python
PARAMS = {
    "minDisparity": 0,
    "numDisparities": 16 * 5,
    "blockSize": 11,
    "disp12MaxDiff": 1,
    "uniquenessRatio": 10,
    "speckleWindowSize": 100,
    "speckleRange": 2,
    "mode": cv2.STEREO_SGBM_MODE_SGBM_3WAY
}
PARAMS["P1"] = 8 * 3 * PARAMS["blockSize"] ** 2
PARAMS["P2"] = 32 * 3 * PARAMS["blockSize"] ** 2
```

- Original #mcl/list-card
  ![3_Archive/1_Attachments/2_imgL.jpg](/img/user/3_Archive/1_Attachments/2_imgL.jpg)
- Undistorted
  ![3_Archive/1_Attachments/2_imgL_undist.jpg](/img/user/3_Archive/1_Attachments/2_imgL_undist.jpg)
- Rectified
  ![3_Archive/1_Attachments/2_imgL_rect.jpg](/img/user/3_Archive/1_Attachments/2_imgL_rect.jpg)
- Disparity map
	![3_Archive/1_Attachments/2_disparity.jpg](/img/user/3_Archive/1_Attachments/2_disparity.jpg)

![3_Archive/1_Attachments/Animation 1.gif](/img/user/3_Archive/1_Attachments/Animation%201.gif)



### Discussion
- `numDisparities` ==16 * 80==과 비교했을 때 ==16 * 5==는 포인트들이 앞 쪽에 몰려있음
- `numDisparities` 가 최대 허용 Disparity 값이라 생각한다면, `numDisparities` 가 작아지는 것은 즉, 최소 허용 Depth 값이 커진다는 의미인데 오히려 포인트들이 앞 쪽에 몰려서 예상을 벗어남
	- *Camera calibration에서 Translation matrix를 보면 -20으로 되어있는데, 혹시 좌우가 바뀌어서 발생하는 문제인가?*

<br/>

## Test 3
```python
# 좌우 반전!!!!!!!

PARAMS = {
    "minDisparity": 0,
    "numDisparities": 16 * 5,
    "blockSize": 11,
    "disp12MaxDiff": 1,
    "uniquenessRatio": 10,
    "speckleWindowSize": 100,
    "speckleRange": 2,
    "mode": cv2.STEREO_SGBM_MODE_SGBM_3WAY
}
PARAMS["P1"] = 8 * 3 * PARAMS["blockSize"] ** 2
PARAMS["P2"] = 32 * 3 * PARAMS["blockSize"] ** 2
```

```
Intrinsic Matrix 1:
[[2.62369756e+03 0.00000000e+00 2.77941317e+03]
 [0.00000000e+00 2.62157243e+03 2.44901503e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 1: 
[[ 0.0080066  -0.06596141  0.00045156  0.00280416  0.06071294]]

Intrinsic Matrix 2: 
[[2.61823793e+03 0.00000000e+00 2.75870357e+03]
 [0.00000000e+00 2.62762659e+03 2.44155682e+03]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00]]

Distortion Coeifficient 2: 
[[-0.01010289 -0.0113979  -0.00127904  0.00286359  0.00717239]]

Rotation Matrix: 
[[ 0.99987996 -0.0134504  -0.00769059]
 [ 0.01358858  0.99974191  0.01820631]
 [ 0.00744372 -0.01830863  0.99980467]]

Translation Matrix: 
[[ 2.01642621e+01]
 [ 1.36751256e-02]
 [-1.25545428e-01]]
```

- Original #mcl/list-card
  ![3_Archive/1_Attachments/3_imgL.jpg](/img/user/3_Archive/1_Attachments/3_imgL.jpg)
- Undistorted
  ![3_Archive/1_Attachments/3_imgL_undist 1.jpg](/img/user/3_Archive/1_Attachments/3_imgL_undist%201.jpg)
- Rectified
  ![3_Archive/1_Attachments/3_imgL_rect.jpg](/img/user/3_Archive/1_Attachments/3_imgL_rect.jpg)
- Disparity map
	![3_Archive/1_Attachments/3_disparity.jpg](/img/user/3_Archive/1_Attachments/3_disparity.jpg)

![3_Archive/1_Attachments/Animation 2.gif](/img/user/3_Archive/1_Attachments/Animation%202.gif)
### Discussion
- 아닌듯 하다!
	- 혹시 disparity가 음수인 부분이 있어서 그런 것 아닐까?
		- 거의 차이점을 찾지 못했으며, 일단 `{python icon}disp[disp<0] = 0` 추가

<br/>

## Test 4
```python
PARAMS = {
    "minDisparity": 0,
    "numDisparities": 16 * 5,
    "blockSize": 11,
    "disp12MaxDiff": 1,
    "uniquenessRatio": 10,
    "speckleWindowSize": 100,
    "speckleRange": 2,
    "mode": cv2.STEREO_SGBM_MODE_SGBM # test에서는 속도를 위해 해당 모드 사용
}
PARAMS["P1"] = 8 * 3 * PARAMS["blockSize"] ** 2
PARAMS["P2"] = 32 * 3 * PARAMS["blockSize"] ** 2
```


- Original #mcl/list-card
  
- Undistorted
  
- Rectified
  
- Disparity map
	


### Discussion
