---
{"dg-publish":true,"permalink":"/0-project/reinforcement-learning/isaac-gym/isaac-gym/","tags":["Project/RL","Study/RL"],"noteIcon":"","created":"2024-12-29"}
---


# Isaac Gym 기본 구조
## Isaac Gym 폴더 구조
- **Isaacgym root folder**
	- **assets**: 로봇 모델, texture, 물체 등 환경의 객체 정의 파일
		- mjcf: MuJoCo modeling XML Format
		- urdf: Unified Robot Description Format
		- textures: 질감에 관련된 이미지
	- **docker**: docker 환경 설치를 위한 파일
	- **docs**: Isaacgym 매뉴얼 파일
	- **licenses**: 라이선스 파일
	- **python**: 실제 개발 환경에서 활용을 위한 라이브러리, 패키지 및 예제 파일
		- **isaacgym**: 라이브러리나 패키지와 관련된 파일이 포함된 폴더

<br/><br/>

# Isaac Gym 예제 분석

```ad-summary
title: Isaac Gym 예제 코드 종류
collapse: true

- **Collision filtering**
  - 파일명: `1080_balls_of_solitude.py`
  - 설명: 멀티 환경에서 각 환경 사이의 ball 객체 간 충돌을 제어할 수 있는 기능을 보임

- **Asset and Environment info**
  - 파일명: `asset_info.py`
  - 설명: IsaacGym에서 URDF나 MJCF 형식의 파일로부터 객체들을 시뮬레이터에 actor로써 로드하고, 각 actor의 정보(body, joint 등)에 접근하고 상태를 체크하는 법을 보여주는 예제

- **Body physics properties example**
  - 파일명: `body_physics_props.py`
  - 설명: 시뮬레이션 환경에 강체(rigid body)를 로드하고 해당 강체에 여러 가지 물리적 속성이나 모양에 변화를 주는 예제

- **Domain Randomization**
  - 파일명: `domain_randomization.py`
  - 설명: 의미론적으로 동일하거나 유사한 사건으로 분류되어 하나의 균질을 형성하는 정보의 단위를 도메인(domain)으로 확률화(randomization)하여 그 정보 데이터셋의 분포를 확장시키기 위한 기능을 보여주는 예제

- **Franka Attractor**
  - 파일명: `franka_attractor.py`
  - 설명: Franka panda 로봇이 target pose에 도달하도록 제어하는 것을 보여주는 예제

- **Isaac Gym Graphics Example**
  - 파일명: `graphics.py`
  - 설명: IsaacGym에서 제공하는 그래픽 관련 기능을 보여주는 예제
    - 예: texture 생성 및 로드, 강체에 적용, 여러 형태의 카메라 이미지 생성

- **DOF Control**
  - 파일명: `dof_controls.py`
  - 설명: Cartpole 에이전트를 이용하여 여러 가지 제어 모드(position, velocity and effort)를 통해 cartpole을 제어하는 예제

- **Joint Monkey**
  - 파일명: `joint_monkey.py`
  - 설명: 지정된 asset을 로드하고 관련된 가용 범위를 보여주는 예제
    - 0~6까지 총 7개의 asset에 대한 예제를 제공

- **Gym Math API**
  - 파일명: `maths.py`
  - 설명: Gym API에서 가장 기본 수학적 타입 표현 및 표현 방법을 보여주는 예제

- **Soft Body**
  - 파일명: `soft_body.py`
  - 설명: Flex backend 시뮬레이션 엔진을 이용한 soft-body 시뮬레이션 예제
    - URDF 포맷의 soft body를 로드하고, 응력(stress)의 세기를 시각화해서 보여주는 예제

- **Visualize Transform**
  - 파일명: `transforms.py`
  - 설명: Cabinet asset를 이용하여 조작을 해보면서 특정 point의 좌표계가 어떻게 변하는지(transform) 보여주는 예제

- **Projectiles**
  - 파일명: `projectiles.py`
  - 설명: 시뮬레이션 도중에 키보드를 이용하여 실시간으로 asset을 소환하고 움직이며, 가상의 블록을 던져서 충돌을 시뮬레이션하는 예제

- **Large mass ratio test**
  - 파일명: `large_mass_ratio.py`
  - 설명: 무거운 박스 쌓기 예제를 통해 시뮬레이션의 안정성을 테스트하는 예제

- **Kuka bin example**
  - 파일명: `kuka_bin.py`
  - 설명: 알레고로 핸드를 부착한 Kuka 로봇을 이용한 물체 시뮬레이션 예제. 물체를 실제로 집는 제어 로직은 별도로 구현해야 함

- **PyTorch Interop**
  - 파일명: `interop_torch.py`
  - 설명: Isaac Gym tensor를 PyTorch와 연동하여 다루는 방법에 대한 예제
    - PyTorch를 이용하여 GPU 메모리에 존재하는 Isaac Gym의 카메라 센서와 물리적 상태 tensor에 접근할 수 있음

- **Franka IK Picking**
  - 파일명: `franka_cube_ik.py`
  - 설명: Franka panda 로봇을 이용하여 큐브를 집는 예제
    - 역기구학을 풀어서 실제로 큐브를 잡는 제어 로직이 탑재되어 있음

- **Franka Operational Space Control**
  - 파일명: `franka_osc.py`
  - 설명: Franka panda 로봇을 이용하여 operational space control을 하는 예제
    - 프로그램에서 로봇 팔 끝(`end-effector`)의 position/orientation의 on/off 옵션 설정 가능

- **Apply Forces**
  - 파일명: `apply_forces.py`
  - 설명: Isaac Gym의 tensor API를 이용하여 강체(rigid body)에 힘(`forces`)이나 회전 힘(`torques`)을 가하는 예제

- **Apply Forces at Positions**
  - 파일명: `apply_forces_at_pos.py`
  - 설명: 강체(rigid body)의 특정 위치를 기준으로 힘(`forces`)이나 회전 힘(`torques`)을 가하는 예제

- **Multiple Cameras**
  - 파일명: `multiple_camera_env.py`
  - 설명: 복수의 환경에서 각 환경마다 복수의 카메라를 활용하는 예제

- **Graphics Up-Axis**
  - 파일명: `test_graphics_up.py`
  - 설명: Up vector를 Y축이나 Z축으로 설정함에 따른 orientation 변화를 확인하는 예제

- **Graphics Materials Example**
  - 파일명: `graphics_materials.py`
  - 설명: 로봇이나 물체 asset을 로드할 때 mesh material 옵션에 따라 달라지는 외형을 확인하는 예제

- **Actor Scaling**
  - 파일명: `actor_scaling.py`
  - 설명: 로봇이나 물체 asset을 로드할 때 스케일을 조절하는 예제

- **Terrain Creation**
  - 파일명: `terrain_creation.py`
  - 설명: 지형(`terrain`) 생성 예제
    - 매개변수를 이용하여 타입이나 높이 등 세부 사항을 변경할 수 있음

- **Spherical Joint**
  - 파일명: `spherical_joint.py`
  - 설명: 구체 관절(`spherical joint`) 시뮬레이션 예제

- **Convex Decomposition**
  - 파일명: `convex_decomposition.py`
  - 설명: 임의의 mesh 물체에 대하여, primitive shape이 아닌 multiple convex shape 설정을 위한 예제

- **Franka Nut Bolt IK Operational Space Control**
  - 파일명: `franka_nut_bolt_ik_osc.py`
  - 설명: Franka panda 로봇을 이용하여 operational space control을 통해 bolt nut 조립 작업을 위한 제어 예제
```

<br/>

```ad-info
title: Common Command Line Options
collapse: true
- `--help`
  - 각 예제의 커맨드라인 옵션을 출력

- `--physx`
  - 시뮬레이션을 위한 물리 엔진으로 PhysX를 사용
  - 강체 바디를 시뮬레이션할 때 사용

- `--flex`
  - 시뮬레이션을 위한 물리 엔진으로 FleX를 사용
  - 소프트 바디를 시뮬레이션할 때 사용

- `--sim_device`
  - PyTorch와 유사한 문법으로 시뮬레이션을 실행할 장치를 선택
    - 예: `cpu` 또는 `cuda` (옵션으로 특정 장치 지정 가능)
    - 기본값: `cuda:0`

- `--pipeline`
  - 텐서 연산을 위한 파이프라인을 선택
    - 선택 가능 값: `cpu` 또는 `gpu`
    - 기본값: `gpu`

- `--graphics_device_id`
  - 그래픽에 사용할 장치의 순번(ordinal)을 지정
```

<br/>

## Collision Filtering (1080_balls_of_solitude.py)

```ad-abstract
36(env) x [(4x4)+(3x3)+(2x2)+1] = 1080
```

![3_Archive/1_Attachments/384498e05aed0a7270275f5fafad11a0_MD5.jpeg](/img/user/3_Archive/1_Attachments/384498e05aed0a7270275f5fafad11a0_MD5.jpeg)

- 다른 색 공들은 충돌하지 않음
	- 다른 색의 공들은 서로 충돌을 하지 않는 것을 볼 수 있는데 이는 IsaacGym에서 환경과 환경 사이에 영향을 줄 수 없도록 기본값으로 설정되어 있음
	- `--all_collisions`
		- 서로 다른 환경끼리 상호작용을 할 수 있음
		  ![3_Archive/1_Attachments/4c4d71ce89dd99ccb3a6f880552c199c_MD5.jpeg](/img/user/3_Archive/1_Attachments/4c4d71ce89dd99ccb3a6f880552c199c_MD5.jpeg)
	- `--no_collisions`
		- 서로 다른 환경 뿐만 아니라 같은 환경 내 객체에서도 충돌을 계산하지 않음
		  ![3_Archive/1_Attachments/5018111af0ac536c2206dead3b0a96bb_MD5.jpeg](/img/user/3_Archive/1_Attachments/5018111af0ac536c2206dead3b0a96bb_MD5.jpeg)

<br/><br/>

## Asset and Environment Info (asset_info.py)

```ad-abstract
title: Introspection API

1. **객체 로드**:
   - URDF 또는 MJCF 형식의 객체(asset)를 로드
   - 로드된 객체의 body, joint, 자유도(degrees of freedom)를 조회 가능

2. **시뮬레이션 상태 조회**:
   - 객체를 시뮬레이션에 actor로 추가한 후, 해당 actor의 현재 상태를 조회 가능
   - 이 과정에서 body, joint 등과 관련된 상태 정보를 확인 가능

```

```shell folded title:Example_Asset_Info

----- Asset info cartpole: -----
Got 3 bodies, 2 joints, and 2 DOFs
Bodies:
  0: 'slider'
  1: 'cart'
  2: 'pole'
Joints:
  0: 'slider_to_cart' (Prismatic)
  1: 'cart_to_pole' (Revolute)
DOFs:
  0: 'slider_to_cart' (Translation)
  1: 'cart_to_pole' (Rotation)

----- Actor: cartpole -----

Bodies
['slider', 'cart', 'pole']
{'cart': 1, 'pole': 2, 'slider': 0}

Joints
['slider_to_cart', 'cart_to_pole']
{'cart_to_pole': 1, 'slider_to_cart': 0}

 Degrees Of Freedom (DOFs)
['slider_to_cart', 'cart_to_pole']
{'cart_to_pole': 1, 'slider_to_cart': 0}

Poses from Body State: # Cartesian coordinates / Quaternion
[((0.        , 0., 0.), (-0.7071068, 0., 0., 0.7071068)) 
 ((0.        , 0., 0.), (-0.7071068, 0., 0., 0.7071068))
 ((0.12000003, 0., 0.), (-0.7071068, 0., 0., 0.7071068))]

Velocities from Body State: # vx, vy, vz, rx, ry, rz
[((0., 0., 0.), (0., 0., 0.)) ((0., 0., 0.), (0., 0., 0.)) 
 ((0., 0., 0.), (0., 0., 0.))]

Body 'slider' has position (0., 0., 0.)
Body 'cart' has position (0., 0., 0.)
Body 'pole' has position (0.12000003, 0., 0.)

DOF states:
[(0., 0.) (0., 0.)]

DOF 'slider_to_cart' has position 0.0
DOF 'cart_to_pole' has position 0.0

```

<br/><br/>

## Body Physics Properties Example (body_physics_props.py)

```ad-abstract
1. **강체 로드**:
   - 속성이 서로 다른 강체 asset을 로드

2. **강체 속성 수정**:
   - 강체의 형태 및 시각적 속성을 수정

3. **강체 제어 및 동작 수행**:
   - 강체 핸들을 사용해 강체를 제어하며 다음과 같은 동작을 수행
     - 강체에 힘(body force) 적용
     - 선형 속도(linear velocity) 설정
```

![3_Archive/1_Attachments/c2822217ca020b7e00d8086b4b18a2b7_MD5.jpeg](/img/user/3_Archive/1_Attachments/c2822217ca020b7e00d8086b4b18a2b7_MD5.jpeg)

<br/><br/>

## Apply Forces (apply_forces.py)

```ad-abstract
Tensor API를 사용하여 강체(rigid body)에 힘(force)과 토크(torque)를 적용
- **참고**: GPU Tensor Pipeline은 현재 PhysX에서만 사용 가능
```

- **Effort**
	- Effort Drvie Mode 로 설정을 한 경우 조인트 타입에 따라 자동으로 Force, Torque 제어 모드로 설정 됨 <br/><br/>
	- **Force**: 선형 조인트(linear joint)의 경우 힘 (단위: $N$, 뉴턴)
		- force_tensor = $[x, y, z]$
		  e.g., $[0.0, 0.0, 300]$
	- **Torque**: 회전 조인트(angular joint)의 경우 토크 (단위: $Nm$, 뉴턴 미터)
		- torque_tensor = $[\alpha, \beta, \gamma]$
		  e.g., $[0.0, 0.0, -100]$
	- **`gym.apply_rigid_body_force_tensors(force_tensor, torque_tensor, coordinate_space)`**
		- **Coordinate space**: {`ENV_SPACE`, `LOCAL_SPACE`, `GLOBAL_SPACE`}
		  ![3_Archive/1_Attachments/a8c6bddbdd5a7335b5827e8bfe60d758_MD5.jpeg](/img/user/3_Archive/1_Attachments/a8c6bddbdd5a7335b5827e8bfe60d758_MD5.jpeg)
			- `ENV_SPACE`: 각 환경에 대한 기준 좌표계
			- `LOCAL_SPACE`: 각 객체에 대한 로컬 좌표계
			- `GLOBAL_SPACE`: 시뮬레이션 환경의 글로벌 좌표계
		- **Center of mass**에서 작용 <br/><br/>



- 객체마다 다른 방향의 힘을 가할 수 있음


<br/><br/>

## Apply Forces at Positions (apply_forces_at_pos.py)

```ad-abstract
Tensor API를 사용하여 강체의 특정 위치에 힘(force)을 적용하는 방법
- **참고**: GPU Tensor Pipeline은 현재 PhysX에서만 사용 가능
```

- **`gym.apply_rigid_body_force_at_pos_tensors(force_tensor, force_position_tensor, coordinate_space)`**
	- **Parameter**
		- Force (단위: $N$, 뉴턴)
			- force_tensor: $[x, y, z]$
			  e.g., $[0.0, 0.0, 400]$
		- Force positions (단위: $m$. 미터)
			- force_position_tensor: $[x, y, z]$
			  e.g., $[0.0, 0.2, 0.0]$
	- **Coordinate space**: {`ENV_SPACE`, `LOCAL_SPACE`, `GLOBAL_SPACE`}
	- **Center of mass**에서 작용 <br/><br/>
