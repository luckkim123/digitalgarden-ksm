---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/3-d-reconstruction-with-mast3r/","tags":["Project","Project/Stereo2PCD"],"noteIcon":"","created":"2024-08-31"}
---

>[!summary] Contents
>
> - [Overview](#Overview)
> 		- [Background](#Background)
> 		- [Purpose](#Purpose)
> 		- [Key Objectives](#Key%20Objectives)
> - [Progress](#Progress)
> 		- [Issues - 알고리즘이 웹 기반으로 구현되어 있음](#Issues%20-%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98%EC%9D%B4%20%EC%9B%B9%20%EA%B8%B0%EB%B0%98%EC%9C%BC%EB%A1%9C%20%EA%B5%AC%ED%98%84%EB%90%98%EC%96%B4%20%EC%9E%88%EC%9D%8C)
> 			- [Solutions](#Solutions)
> 		- [Issues - GLB 포맷으로 결과 출력](#Issues%20-%20GLB%20%ED%8F%AC%EB%A7%B7%EC%9C%BC%EB%A1%9C%20%EA%B2%B0%EA%B3%BC%20%EC%B6%9C%EB%A0%A5)
> 			- [Solutions](#Solutions)
> 		- [Issues - PCD 데이터의 좌표계가 고정되지 않음](#Issues%20-%20PCD%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98%20%EC%A2%8C%ED%91%9C%EA%B3%84%EA%B0%80%20%EA%B3%A0%EC%A0%95%EB%90%98%EC%A7%80%20%EC%95%8A%EC%9D%8C)
> 			- [Root Cause Analysis](#Root%20Cause%20Analysis)
> 			- [Solutions](#Solutions)
> 		- [Issues - PCD 데이터의 Scale 문제](#Issues%20-%20PCD%20%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98%20Scale%20%EB%AC%B8%EC%A0%9C)
> 			- [Root Cause Analysis](#Root%20Cause%20Analysis)
> 			- [Solutions](#Solutions)
> - [Resource](#Resource)

<br>


# Overview

### Background
- 연구 목표:
	- 수중환경에서 스테레오 카메라를 사용한 [[0_Project/00_Research Internship/001_3D Reconstruction/3D Reconstruction from Stereo Images\|3D Reconstruction]]
- 초기에는 Stereo calibration 후 [[2_Resource/1_Study/1_Coding/OpenCV/stereoSGBM_create\|Stereo SGBM]] 방법을 사용하여 PCD 생성을 시도
	- 물체의 크기, 거리, 이미지 배경의 복잡성 등 특정 환경 조건에서 포인트 클라우드를 정확하게 추출하지 못하는 문제가 발생 ([[0_Project/00_Research Internship/001_3D Reconstruction/Ablation Study for 3D Reconstruction\|Ablation Study for 3D Reconstruction]])
- 이에, 더 나은 방법을 탐색 중 Naver Lab에서 개발한 MASt3R 알고리즘을 발견하고 연구에 적용하기로 결정

<br/>

### Purpose
- 수중 환경에서 스테레오 카메라를 이용해 정확한 3D reconstruction을 수행

<br/>

### Key Objectives
- 기존 Stereo SGBM 방법의 한계를 극복하고, MASt3R 알고리즘을 통해 PCD 추출의 정확도 향상
- MASt3R 알고리즘을 웹 기반이 아닌 코드 레벨에서 실험할 수 있도록 수정하고, 결과 데이터를 GLB 포맷이 아닌 PCD 포맷으로 변환하여 사용 편의성 향상
- PCD의 Origin 이 고정되지 않는 문제와 Scale 문제 해결
	- 결과적으로 KIRO 수조의 랜드마크에서 추출한 PCD가 월드 좌표계에 고정된 상태로 생성되는 Sequence 데이터 생성

<br/><br/>

# Progress
### Issues - 알고리즘이 웹 기반으로 구현되어 있음 
- 기존 코드는 웹 기반으로 구현되어 있어 실험을 하는데 어려움이 있음
>[!multi-column]
>>![3_Archive/1_Attachments/Pasted image 20240831194345.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240831194345.png)
>
>>![3_Archive/1_Attachments/Pasted image 20240831194453.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240831194453.png)

<br/>

#### Solutions
- MASt3R의 소스 코드에서 `gradio`를 사용하여 웹 기반 애플리케이션을 생성하는 부분을 수정하여, 코드 레벨에서 실험을 할 수 있도록 수정

```python fold title:mast3r/demo.py
def main_demo(indir, outdir, position_data, model, device, image_size, 
			  silent=False, gradio_delete_cache=False):
    lr1 = 0.07 	# 이 값은 초기 global alignment의 학습 속도를 조절
    niter1 = 500 # Coarse alignment를 수행하는 동안의 반복 횟수
    lr2 = 0.014 # 정밀한 정렬을 위한 학습 속도를 조절
    niter2 = 200 # Fine alignment를 수행하는 동안의 반복 횟수
    optim_level = "refine+depth" # "coarse", "refine", "refine+depth"
    matching_conf_thr = 5.0 # 매칭 신뢰도 임계값을 설정
    shared_intrinsics = True # 모든 카메라가 동일한 내부 파라미터 공유
    scenegraph_type = "stereo" # 이미지 페어링 방법을 정의
    ''' scenegraph_type
    Define how to make pairs
    
    complete: all possible image pairs
    stereo: pairing each frame of stereo images
    swin: sliding window
    logwin: sliding window with long range
    oneref: match one image with all
    '''
    min_conf_thr = 1.5 # 포인트 클라우드를 생성할 때 사용할 최소 신뢰도 임계값
    cam_size = 0.2 # 카메라를 시각화할 때의 크기를 설정
    TSDF_thresh = 0.0 # TSDF(Truncated Signed Distance Function) 임계값을 설정
    mask_sky = False # 하늘 영역을 마스킹할지 여부를 설정
    clean_depth = True # 깊이 맵의 클린업 여부를 설정
    scenegraph_flag = False # Scenegraph 옵션이 이미 설정되었는지 여부를 확인
    scene = SparseGAState(None) # Sparse Global Alignment 상태 객체를 초기화

    winsize = 1
    win_cyclic = False
    refid = 0
    inputfiles = []
    
    for idx, image_name in enumerate(sorted(os.listdir(os.path.join(indir, "left")))):
        if image_name in os.listdir(os.path.join(indir, "right")):
            os.makedirs(outdir, exist_ok=True)
            # 이미지를 입력 파일 리스트에 추가
            inputfiles.append(os.path.join(indir, "left", image_name))
            inputfiles.append(os.path.join(indir, "right", image_name))
            if len(inputfiles) == 2:
                # 특정 scenegraph_type에 대해 옵션을 설정
                if scenegraph_type in ["swin", "logwin", "oneref"] \
                	and not scenegraph_flag: 
                    winsize, win_cyclic, refid, scenegraph_flag =\
                    	set_scenegraph_options(inputfiles, scenegraph_type,
                                               win_cyclic, winsize, refid)
                # get_reconstructed_scene 함수를 호출하여 3D 재구성을 수행
                get_reconstructed_scene(outdir, position_data, 
                                        gradio_delete_cache, model, device, 
                                        silent, image_size, scene, inputfiles,
                                        optim_level, lr1, niter1, lr2, niter2,
                                        min_conf_thr, matching_conf_thr, mask_sky,
                                        clean_depth,cam_size, scenegraph_type,
                                        winsize, win_cyclic, refid,TSDF_thresh,
                                        shared_intrinsics)
            # 이미지 쌍 처리가 끝나면 리스트를 초기화
            elif len(inputfiles) > 2:
                inputfiles.clear()
```

<br/><br/>

### Issues - GLB 포맷으로 결과 출력
- MASt3R 소스 코드는 PCD 데이터가 GLB 형식으로 출력되었음
>[!info] GLB format
>- 3D 모델 데이터를 효율적으로 저장하고 전송하기 위한 파일 형식
>- GLTF (GL Transmission Format)의 Binary 형식으로, GLTF 파일과 같은 데이터를 포함하지만 모든 데이터를 하나의 이진 파일로 압축하여 저장

- Python 및 ROS에서 해당 포맷의 데이터를 다루는 라이브러리가 제공되지 않기 때문에 데이터를 Open3d 및 PCL에서 다루는 데이터 포맷인 PLY 혹은 PCD 형태로 변경할 필요가 있음

<br/>

#### Solutions
- 포인트 클라우드를 저장하는 부분에서 포인트의 좌표 정보와 색상 정보를 Open3d 가 데이터를 다루는 형태로 변경한 후 PCD 포맷으로 저장하도록 코드 수정

```python fold title:mast3r/demo.py
import numpy as np
import open3d as o3d

# (omitted)

def _convert_scene_output_to_pcd(outfile, imgs, pts3d, mask, focals, cams2world, cam_size=0.05, cam_color=None, as_pointcloud=False, transparent_cams=False, silent=False):
    
    # (omitted)
    
    # Save as PCD
    pts = np.concatenate([p[m.ravel()] for p, m in zip(pts3d, mask)]).reshape(-1, 3)
    col = np.concatenate([p[m] for p, m in zip(imgs, mask)]).reshape(-1, 3)
    
    # Add camera positions and colors for visualization purposes
    pts = np.vstack((pts, cams2world[0, :3, 3], cams2world[1, :3, 3])).reshape(-1, 3)
    col = np.vstack((col, np.array([255, 0, 0]), np.array([0, 0, 255])))
    
    # Exclude points with infinite values
    valid_msk = np.isfinite(pts.sum(axis=1))
    
    # Create PCD data using Open3D's data format
    pcd = o3d.geometry.PointCloud()
    v3d = o3d.utility.Vector3dVector
    
    pcd.points = v3d(pts[valid_msk].astype(np.float64))
    pcd.colors = v3d(col[valid_msk].astype(np.float64))
    
    # Do not save if the number of points is less than 100
    if len(np.asarray(pcd.points)) < 100:
        print(pcd)
        return outfile

    # (omitted)
    
    print("Length of Baseline: ", baseline)
    if not silent:
        print('(exporting 3D PCD to', outfile + ".pcd", ')')
    scene.export(file_obj=outfile + ".glb")
    return outfile

```

<br/><br/>

### Issues - PCD 데이터의 좌표계가 고정되지 않음

![coord_1.gif](/img/user/3_Archive/1_Attachments/coord_1.gif)

<br/>

#### Root Cause Analysis
- MASt3R 알고리즘에서는 입력된 여러 이미지 중 하나를 기준 이미지로 설정하고, 각각의 이미지에서 추출한 포인트 클라우드와 기준 이미지에서 추출한 포인트 클라우드를 Sparse Global Alignment 알고리즘에 적용하여 각 카메라 위치에 대한 상대적인 회전(Rotation)과 이동(Translation)을 계산
- 또한, 기준 이미지와 월드 좌표계 사이의 R, T 행렬을 계산하는데, 이때 변환 행렬이 일정하지 않기 때문에 PCD 데이터의 좌표계가 일정하게 고정되지 않는 문제 발생

<br>

#### Solutions
- Stereo 이미지와 같이 취득된 Cyclops 위치 정보를 기준 카메라의 위치로 가정하고, 해당 위치로 카메라 좌표계를 변환
- 이를 통해 물체는 월드 좌표계에 고정되며, 카메라 좌표계는 로봇이 실제로 이동하고 회전한만큼 이동하도록 수정

```python title:sparse_ga.py fold
class SparseGA():
  # 로봇의 위치 정보가 담긴 txt 파일에서 현재 rostime과 가장 유사한 로봇 위치 정보를 읽음
  def get_abs_im_poses(self):
      df = pd.read_csv(self.position_data)
      target_time = float(self.img_paths[self.mst[0]].split("/")[-1].split(".")[0])
      target_idx = (df["time"] - target_time).abs().idxmin()
      target_row = df.iloc[target_idx]
      return target_row["X"], target_row["Y"], target_row["Z"], \
    		target_row["Roll"], target_row["Pitch"], target_row["Yaw"]

  # 위치 정보가 들어왔을 때 카메라 좌표계를 해당 위치로 이동
  def shift_im_poses(self, x=0, y=0, z=0, roll=0, pitch=0, yaw=0):
      R_roll = torch.tensor([[1, 0, 0], 
                             [0, math.cos(roll), -math.sin(roll)],
                             [0, math.sin(roll), math.cos(roll)]], 
                            dtype = torch.float32, device = "cuda")
      R_pitch = torch.tensor([[math.cos(pitch), 0, math.sin(pitch)],
                              [0, 1, 0],
                              [-math.sin(pitch), 0, math.cos(pitch)]], 
                             dtype = torch.float32, device = "cuda")
      R_yaw = torch.tensor([[math.cos(yaw), -math.sin(yaw), 0],
                            [math.sin(yaw), math.cos(yaw), 0],
                            [0, 0, 1]], dtype = torch.float32, device = "cuda")
      R = R_yaw @ R_pitch @ R_roll
      T = torch.tensor([x, y, z], dtype = torch.float32, device = "cuda")
      T = T - R @ self.cam2w[0, :3, 3]
      M = torch.eye(4, dtype = torch.float32, device = "cuda")
      M[:3, :3] = R
      M[:3, 3] = T
      self.cam2w = M @ self.cam2w
        
  def get_im_poses(self):
	  # 카메라 좌표계를 월드 좌표계의 원점으로 이동
      self.shift_im_poses(yaw=math.pi/2)
      self.shift_im_poses(pitch=math.pi/2)

	  # 로봇의 위치 정보 읽음
      x, y, z, roll, pitch, yaw = self.get_abs_im_poses()

	  # 해당 로봇의 위치로 카메라 좌표계 이동
      self.shift_im_poses(roll*math.pi/180, pitch*math.pi/180, yaw*math.pi/180)

	  # Stereo camera가 로봇에 pitch 방향으로 30도 회정해서 부착되어 있음
      self.shift_im_poses(x, y, z, pitch=math.pi/6)
      return self.cam2w
```

![shifted_coord.gif](/img/user/3_Archive/1_Attachments/shifted_coord.gif)

<br/><br/>

### Issues - PCD 데이터의 Scale 문제
- 위 영상 처럼 Landmark의 크기 및 거리가 실제보다 작게 나타나는 문제


<br/>

#### Root Cause Analysis
- MASt3R 알고리즘에서는 Optimization을 원활하게 진행하기 위해 Iteration 과정 중에 Translation 파라미터를 의도적으로 Downscale함
- 이로 인해 PCD 데이터에서도 Downscaling이 발생하며, 실제보다 작은 거리로 나타나는 문제가 발생

```python fold title:sparse_ga.py
def sparse_scene_optimizer():
  # 중략
  
  def make_K_cam_depth(log_focals, pps, trans, quats, log_sizes, core_depth):
    # 중략
    
    # smart reparameterizaton of cameras
    trans_offset = z_cameras.unsqueeze(1) * torch.cat((imsizes / focals.unsqueeze(1) * (0.5 - pps), ones), dim=-1)
    new_trans = global_scaling * (tmp_cam2w[:, :3, 3:4] - tmp_cam2w[:, :3, :3] @ trans_offset.unsqueeze(-1))
    cam2w = torch.cat((torch.cat((tmp_cam2w[:, :3, :3], new_trans), dim=2),
                      vec0001.view(1, 1, 4).expand(len(K), 1, 4)), dim=1)
```

<br>

#### Solutions
- camera to world 변환 행렬을 확인해본 결과 Baseline 이 실제 보다 작게 추정되는 것을 확인하였으며, Downscaling 비율이 PCD 데이터의 Downscaling 비율과 유사한 것을 확인 ([[2_Resource/1_Study/5_Sensors/Stereo Camera/Stereo Camera Depth Estimation#Depth Estimation\|Stereo Camera Depth Estimation]])
- 이를 통해 각 포인트들의 x, y, z 좌표를 Baseline 기준으로 Downscaling 된 비율만큼 Upscaling하여 최종적으로 실제 크기에 맞게 조정

```python fold title:mst3r/demo.py
def _convert_scene_output_to_pcd(outfile, imgs, pts3d, mask, focals, cams2world, 
								 cam_size=0.05, cam_color=None, as_pointcloud=False, 
								 transparent_cams=False, silent=False):
  	# 중략
    
    baseline = np.sqrt(np.sum(np.square(cams2world[0, :3, 3] - cams2world[1, :3, 3])))
    
    # Save as pcd
    pts = np.concatenate([p[m.ravel()] for p, m in zip(pts3d, mask)]).reshape(-1, 3)
    tmp = pts - cams2world[0, :3, 3]
    tmp *= 0.2 / baseline
    pts = cams2world[0, :3, 3] + tmp
    col = np.concatenate([p[m] for p, m in zip(imgs, mask)]).reshape(-1, 3)
```

![final.gif](/img/user/3_Archive/1_Attachments/final.gif)

<br/><br/>

# Resource
- [[3_Archive/0_Fleeting Notes/MASt3R 알고리즘 (작성중)\|MASt3R 알고리즘 (작성중)]]
- [[MASt3R 코드 분석\|MASt3R 코드 분석]]
- [[3_Archive/0_Fleeting Notes/Camera Calibration (작성중)\|Camera Calibration (작성중)]]