---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/extract-pcd-from-stereo-images-open-cv/","tags":["Study/Coding","Project/Stereo2PCD"],"noteIcon":"","created":"2024-06-27"}
---


```python
def write_ply(fn, verts, colors):

	verts = verts.reshape(-1, 3)
	colors = colors.reshape(-1, 3)
	verts = np.hstack([verts, colors])
	
	with open(fn, 'wb') as f:
		f.write((ply_header % dict(vert_num=len(verts))).encode('utf-8'))
		np.savetxt(f, verts, fmt='%f %f %f %d %d %d ')
```


```python
def main():

	print('loading images...')
	
	imgL = cv2.imread("/workspace/dataset/processed/left/000100.jpg", 0)
	imgR = cv2.imread("/workspace/dataset/processed/right/000100.jpg", 0)
	
	imgL = cv2.resize(imgL, (500, 500))
	imgR = cv2.resize(imgR, (500, 500))
	
	# disparity range is tuned for 'aloe' image pair
	window_size = 3
	min_disp = 16
	num_disp = 112-min_disp
	
	stereo = cv2.StereoSGBM_create(
		minDisparity = min_disp,
		numDisparities = num_disp,
		blockSize = 16,
		P1 = 8*3*window_size**2,
		P2 = 32*3*window_size**2,
		disp12MaxDiff = 1,
		uniquenessRatio = 10,
		speckleWindowSize = 100,
		speckleRange = 32
	)
	
	print('computing disparity...')
	disp = stereo.compute(imgL, imgR).astype(np.float32) / 16.0
	
	print('generating 3d point cloud...',)
	h, w = imgL.shape[:2]
	f = 0.8*w # guess for focal length
	Q = np.float32(
		[[1, 0, 0, -0.5*w],
		[0,-1, 0, 0.5*h], # turn points 180 deg around x-axis,
		[0, 0, 0, -f], # so that y-axis looks up
		[0, 0, 1, 0]]
	)
	points = cv2.reprojectImageTo3D(disp, Q)
	colors = cv2.cvtColor(imgL, cv.COLOR_BGR2RGB)
	mask = disp > disp.min()
	out_points = points[mask]
	out_colors = colors[mask]
	out_fn = 'out.ply'
	
	write_ply(out_fn, out_points, out_colors)
	print('%s saved' % out_fn)
	
	cv2.imshow('left', imgL)
	cv2.imshow('disparity', (disp-min_disp)/num_disp)
	cv2.waitKey()
	
	print('Done')
```

## cv2.StereoSGBM_create 파라미터
- `minDisparity`
	- 가능한 최소한의 [[disparity\|disparity]] 값
	- 보통 0으로 설정하지만 조정 알고리즘이 이미지를 이동시킬 수 있어서 알맞게 조정해야함
- `numDisparities`
	- Disparity 의 범위 설정
	- 16 배수여야 하며, 최소 Disparity 에서 최대 Disparity 까지의 범위
- `blockSize`
	- 매칭을 수행할 때 사용하는 블록(패치)의 크기 지정
	  ```ad-tip
	  collapse: true
	  - 블록 매칭
		  - 두 이미지에서 유사한 블록을 찾아 Disparity 를 계산하는 과정
		  - 작을수록 더 세밀한 매칭을 가능하게 하지만, 노이즈에 민감할 수 있음
	  ```

	- 홀수여야 하며, 일반적으로 3~11 사이의 값 사용
- `P1`
	- Disparity map 을 생성할 때 사용되는 Smoothness 를 조절하는 파라미터
	- 일반적으로 `8 * # of channels * blockSize ** 2` 로 설정
- `P2`
	- Smoothness 를 조절하는 두 번째 파라미터
	- 일반적으로 `32 * # of channels * blockSize ** 2` 로 설정
- `disp12MaxDiff`
	- 좌우 Disparity map 의 최대 허용 차이
	- 0 또는 음수로 설정할 경우 해당 검사 생략
- `uniquenessRatio`
	- 1등 매치와 2등 매치간의 마진을 퍼센트로 나타낸 값
	- 일반적으로 5~15 사이 값
- `speckleWindowSize`
	- 작은 점 노이즈 (Speckle) 를 제거하기 위한 창의 크기
	- 0으로 설정하면 해당 검사 생략
	- 일반적으로 5~200 사이 값
- `speckleRange`
	- Speckle 제거를 위한 Disparity 범위를 설정
		- Speckle 내 모든 Disparity 는 이 값을 초과하지 않아야 함
	- 0으로 설정하면 해당 검사 생략
	- 일반적으로 1, 2
- `preFilterCap`
	- 입력 이미지의 사전 필터링을 위한 최대 값
	- 일반적으로 31
- `mode`
	- `cv2.STEREO_SGBM_MODE_SGBM`
	- `cv2.STEREO_SGBM_MODE_HH`
	- `cv2.STEREO_SGBM_MODE_SGBM_3WAY`
	- `cv2.STEREO_SGBM_MODE_HH4`