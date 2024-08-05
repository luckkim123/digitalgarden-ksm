---
{"dg-publish":true,"permalink":"/3-archive/30-fleeting-notes/hyperparameter-tunning/","tags":["Project/Stereo2PCD"],"noteIcon":"","created":"2024-08-05"}
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
MIN_DISP = 0
NUM_DISP = 16 * 80
BLOCK_SIZE = 11 # 3 ~ 11
P1 = 8 * 3 * BLOCK_SIZE ** 2
P2 = 32 * 3 * BLOCK_SIZE ** 2
DISP_MAX_DIFF = 1 # Inactive: 0
UNIQUENESS = 10 # 5~15
SPECKLE_WIN_SIZE = 100 # Inactive: 0 / 50~200
SPECKLE_RANGE = 2 # 1 or 2
```

- Original #mcl/list-card
  ![3_Archive/31_Attachments/1_imgL.jpg](/img/user/3_Archive/31_Attachments/1_imgL.jpg)
- Undistorted
  ![3_Archive/31_Attachments/1_imgL_undist.jpg](/img/user/3_Archive/31_Attachments/1_imgL_undist.jpg)
- Rectified
  ![3_Archive/31_Attachments/1_imgL_rect.jpg](/img/user/3_Archive/31_Attachments/1_imgL_rect.jpg)
- Disparity map
	![3_Archive/31_Attachments/1_disparity.jpg](/img/user/3_Archive/31_Attachments/1_disparity.jpg)


![3_Archive/31_Attachments/Animation.gif](/img/user/3_Archive/31_Attachments/Animation.gif)