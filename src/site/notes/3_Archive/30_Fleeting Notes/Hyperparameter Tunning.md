---
{"dg-publish":true,"permalink":"/3-archive/30-fleeting-notes/hyperparameter-tunning/","tags":["Project/Stereo2PCD"],"noteIcon":"","created":"2024-08-05"}
---

- test 1
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
	
	![3_Archive/31_Attachments/1_imgL.jpg|+grid](/img/user/3_Archive/31_Attachments/1_imgL.jpg)![3_Archive/31_Attachments/1_imgL_undist.jpg|+grid](/img/user/3_Archive/31_Attachments/1_imgL_undist.jpg)
	<center style="font-size: 12; opacity: 0.7">Original / Undistorted</center>
	
	![3_Archive/31_Attachments/1_imgL_rect.jpg|+grid](/img/user/3_Archive/31_Attachments/1_imgL_rect.jpg)![3_Archive/31_Attachments/1_disparity.jpg|+grid](/img/user/3_Archive/31_Attachments/1_disparity.jpg)
	<center style="font-size: 12; opacity: 0.7">Rectified / Disparity map</center>
	
![3_Archive/31_Attachments/2024-08-05101255-ezgif.com-video-to-gif-converter.gif](/img/user/3_Archive/31_Attachments/2024-08-05101255-ezgif.com-video-to-gif-converter.gif)

![[3_Archive/31_Attachments/녹음 2024-08-05 101255.mp4]]



