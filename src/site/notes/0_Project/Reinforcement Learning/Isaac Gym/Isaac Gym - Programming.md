---
{"dg-publish":true,"permalink":"/0-project/reinforcement-learning/isaac-gym/isaac-gym-programming/","tags":["Study/RL","Project/RL"],"noteIcon":"","created":"2024-12-29"}
---


# Simulation Setup

- Isaac Gym은 **지능형 에이전트를 훈련하기 위한 동적 환경을 생성**할 수 있는 시뮬레이션 인터페이스를 제공
- 이 API는 객체 지향 방식이 아닌 **절차적, 데이터 중심적**으로 설계되어, C++로 구현된 코어와 Python으로 작성된 클라이언트 스크립트 간의 효율적인 정보 교환이 가능

<br/>

1. **데이터 구조**:
    - Isaac Gym은 **계층적인 객체 구조** 대신 **평면 데이터 배열(flat data arrays)**을 사용하여 상태 및 제어 데이터를 표현.
    - 이를 통해 Python 라이브러리(예: NumPy)로 데이터를 쉽게 조작 가능.
    - CPU 또는 GPU 텐서 형태로 데이터를 제공하여 PyTorch와 같은 딥러닝 프레임워크와의 통합 가능.

1. **기본 API**:
    - API는 `gymapi` 모듈에 정의.
    - Gym API의 모든 함수는 **싱글톤 객체**를 통해 접근 가능:
        
        ```python
        from isaacgym import gymapi
        gym = gymapi.acquire_gym()  # Gym API 객체 생성
        ```
        

<br/>

## Creating a Simulation

1. **시뮬레이터 생성**:
    - `create_sim` 메서드를 사용하여 시뮬레이션 생성:
        
        ```python
        sim_params = gymapi.SimParams()
        sim = gym.create_sim(compute_device_id, graphics_device_id, gymapi.SIM_PHYSX, sim_params)
        ```
        
    - `sim` 객체는 물리 및 그래픽 컨텍스트를 포함하여 에셋 로드, 환경 생성, 시뮬레이션과 상호작용 가능.

1. **매개변수 설명**:
    - **첫 번째 인자**:
        - **`compute_device_id`**: 물리 시뮬레이션에 사용할 GPU ID.
    - **두 번째 인자**:
        - **`graphics_device_id`**: 렌더링에 사용할 GPU ID.
        - 헤드리스(headless) 시뮬레이션의 경우 `-1`로 설정하면 그래픽 컨텍스트를 생성하지 않음.
    - **세 번째 인자**:
        - **물리 엔진 선택**:
            - `SIM_PHYSX`: CPU/GPU에서 실행되는 강체 및 관절 시뮬레이션(새로운 텐서 API 완벽 지원).
            - `SIM_FLEX`: GPU에서 실행되는 연체(body) 및 강체 시뮬레이션(텐서 API는 아직 완벽 지원 X).
    - **네 번째 인자**:
        - **`sim_params`**: 추가 시뮬레이션 매개변수.

```ad-tip
title: **PhysX v.s. Flex**

1. **PhysX**:
    - CPU와 GPU 모두에서 실행 가능.
    - 강체 및 관절 시뮬레이션 지원.
    - 텐서 API를 완벽히 지원.
2. **Flex**:
    - GPU에서만 실행.
    - 연체(body) 및 강체 시뮬레이션 지원.
    - 텐서 API는 아직 제한적으로 지원.
```

<br/>

### Simulation Parameters

```python fold

# get default set of parameters
sim_params = gymapi.SimParams()

# set common parameters
sim_params.dt = 1 / 60
sim_params.substeps = 2
sim_params.up_axis = gymapi.UP_AXIS_Z
sim_params.gravity = gymapi.Vec3(0.0, 0.0, -9.8)

# set PhysX-specific parameters
sim_params.physx.use_gpu = True
sim_params.physx.solver_type = 1
sim_params.physx.num_position_iterations = 6
sim_params.physx.num_velocity_iterations = 1
sim_params.physx.contact_offset = 0.01
sim_params.physx.rest_offset = 0.0

# set Flex-specific parameters
sim_params.flex.solver_type = 5
sim_params.flex.num_outer_iterations = 4
sim_params.flex.num_inner_iterations = 20
sim_params.flex.relaxation = 0.8
sim_params.flex.warm_start = 0.5

# create sim with these parameters
sim = gym.create_sim(compute_device_id, graphics_device_id, physics_engine, sim_params)
```

#### Common Parameters
- **`dt` (시간 간격)**: 시뮬레이션의 시간 간격.  
    예: `sim_params.dt = 1 / 60` (60Hz 시뮬레이션 속도)
- **`substeps` (서브스텝)**: 각 시뮬레이션 단계에서 계산되는 세부 스텝 수.  
    예: `sim_params.substeps = 2`
- **`up_axis` (업축 방향)**: 시뮬레이션의 업축을 설정.  
    예: `sim_params.up_axis = gymapi.UP_AXIS_Z` (z축 업 방향)
- **`gravity` (중력 설정)**: 중력 벡터를 설정.  
    예: `sim_params.gravity = gymapi.Vec3(0.0, 0.0, -9.8)`

<br/>

#### PhysX-specific Parameters
- **`use_gpu`**: GPU를 사용할지 여부.  
    예: `sim_params.physx.use_gpu = True`
- **`solver_type`**: 물리 계산 솔버 타입.  
    예: `sim_params.physx.solver_type = 1`
- **`num_position_iterations`**: 위치 보정 반복 횟수.  
    예: `sim_params.physx.num_position_iterations = 6`
- **`num_velocity_iterations`**: 속도 보정 반복 횟수.  
    예: `sim_params.physx.num_velocity_iterations = 1`
- **`contact_offset` 및 `rest_offset`**: 충돌 처리와 관련된 오프셋 값.  
    예:
    
    ```python
    sim_params.physx.contact_offset = 0.01
    sim_params.physx.rest_offset = 0.0
    ```
    
<br/>

#### Flex-specific Parameters
- **`solver_type`**: Flex 전용 솔버 타입.  
    예: `sim_params.flex.solver_type = 5`
- **`num_outer_iterations` 및 `num_inner_iterations`**: 외부 및 내부 반복 횟수 설정.  
    예:
    
    ```python
    sim_params.flex.num_outer_iterations = 4
    sim_params.flex.num_inner_iterations = 20
    ```
    
- **`relaxation`**: 물리 시뮬레이션의 완화 정도.  
    예: `sim_params.flex.relaxation = 0.8`
- **`warm_start`**: Flex 초기 조건 설정.  
    예: `sim_params.flex.warm_start = 0.5`

<br/>

#### Up Axis

- Isaac Gym은 **y-up**과 **z-up** 시뮬레이션을 모두 지원하며, 일반적으로 **z-up** 사용
    ```python
    sim_params.up_axis = gymapi.UP_AXIS_Z
    sim_params.gravity = gymapi.Vec3(0.0, 0.0, -9.8)
    ```
    
- **y-up**은 Isaac Gym의 기본값이지만 향후 변경될 가능성이 있음.
- 업축 설정 외에도 **지면(ground plane)** 생성 시 별도 주의 필요.

<br/>

### Creating a Ground Plane

```python fold

# 지면 설정
plane_params = gymapi.PlaneParams()
plane_params.normal = gymapi.Vec3(0, 0, 1)  # z-up 지면
plane_params.distance = 0
plane_params.static_friction = 1           # 정지 마찰 계수
plane_params.dynamic_friction = 1          # 동적 마찰 계수
plane_params.restitution = 0               # 반발 계수 (탄성 없음)

# 지면 생성
gym.add_ground(sim, plane_params)
```

#### Ground Plane Configuration

- `gymapi.PlaneParams()`
	- 지면의 속성을 설정
- **`normal` (법선 벡터)**:
    - 지면의 방향을 정의.
    - 업축 선택에 따라 달라짐:
        - `z-up`: `gymapi.Vec3(0, 0, 1)`
        - `y-up`: `gymapi.Vec3(0, 1, 0)`
    - 축 방향이 아닌 기울어진 지면도 설정 가능.
- **`distance` (거리)**:
    - 원점에서 지면까지의 거리.  
        - 예: `plane_params.distance = 0`
- **`static_friction` (정지 마찰 계수)**:
    - 물체가 지면에서 움직이기 시작하는 데 필요한 마찰력.  
        - 예: `plane_params.static_friction = 1`
- **`dynamic_friction` (동적 마찰 계수)**:
    - 물체가 지면 위를 움직일 때 발생하는 마찰력.  
        - 예: `plane_params.dynamic_friction = 1`
- **`restitution` (반발 계수)**:
    - 물체가 지면과 충돌 시 얼마나 튕겨 나가는지를 결정.  
        - 예: `plane_params.restitution = 0` (탄성 없음)

<br/><br/>

## Loading Assets

- Isaac Gym은 **URDF** 및 **MJCF** 파일 형식을 지원
- 이를 통해 물체, 충돌 형태, 시각적 부착물, 관절, 자유도(DOF) 등의 정의를 포함하는 **GymAsset 객체**를 생성
- 일부 형식에서는 연체(body)와 입자(particle)도 지원
- 에셋을 로드하면 **GymAsset 객체**가 생성되며, 이는 모델의 물리적 및 시각적 정의를 포함

```python
asset_root = "../../assets"
asset_file = "urdf/franka_description/robots/franka_panda.urdf"
asset = gym.load_asset(sim, asset_root, asset_file)
```

### AssetOptions
- **`fix_base_link`**:
    - 기본 링크를 고정할지 여부.
    - 예: `asset_options.fix_base_link = True`
- **`armature`**:
    - 모델의 관절 강성 값을 설정.
    - 예: `asset_options.armature = 0.01`

```python
asset_options = gymapi.AssetOptions()
asset_options.fix_base_link = True
asset_options.armature = 0.01

asset = gym.load_asset(sim, asset_root, asset_file, asset_options)
```

### Loading Assets and Simulation

- **에셋 로드**는 시뮬레이션에 즉시 추가되지 않음.
- GymAsset은 **설계도(blueprint)** 역할을 하며, 여러 번 인스턴스화 가능.
    - 각각의 인스턴스는 다른 **포즈(pose)**와 **속성(properties)**를 가질 수 있음.

```python
# 로드된 에셋을 시뮬레이션 환경에 추가
pose = gymapi.Transform()  # 기본 위치 설정
actor_handle = gym.create_actor(env, asset, pose, "actor_name")
```

<br/><br/>

## Environments and Actors

- Isaac Gym에서 **환경(environment)**은 물리적으로 상호작용하는 액터(actor)와 센서(sensor)들로 구성된 시뮬레이션 단위
	- **액터(Actors)**:
	    - 환경 내에서 물리적으로 상호작용하는 객체들.
	    - 상태는 물리 엔진이 유지하며, 제어 API를 통해 상태 조작 가능.
	- **센서(Sensors)**:
	    - 카메라와 같은 센서를 환경에 배치하여, 해당 환경의 액터를 캡처 가능.

<br/>

### Multiple Environments

- Isaac Gym은 **여러 환경을 하나의 시뮬레이션에 병합**하여 동시에 실행 가능
- 이 기능은 특히 **강화 학습**과 같이 대량의 반복 실행이 필요한 응용 분야에서 중요

<br/>

- **주요 특징**:
	1. **병렬 실행**:
	    - 수십, 수백, 또는 수천 개의 환경을 GPU에서 동시에 실행 가능.
	    - 각 환경은 독립적이며, 물리적 상호작용이 분리됨.
	2. **랜덤화**:
	    - 초기 조건(배치, 액터 위치, 액터 종류 등)을 환경마다 다르게 설정 가능.
	    - 물리적, 시각적, 제어 속성을 환경마다 다르게 조정 가능.
	3. **성능 향상**:
	    - 다수의 단순 환경을 하나의 시뮬레이션에 병합하면 오버헤드가 줄어들고, 유의미한 계산에 더 많은 시간을 할애 가능.
	    - 예: 로봇 팔이 물건을 집는 작업이나 휴머노이드 모델이 걷는 작업 학습.

<br/>

### Create Environment

```python
spacing = 2.0
lower = gymapi.Vec3(-spacing, 0.0, -spacing)  # 환경의 하단 좌표
upper = gymapi.Vec3(spacing, spacing, spacing)  # 환경의 상단 좌표

env = gym.create_env(sim, lower, upper, 8)  # 환경 생성
```

- **`lower`**와 **`upper`**:
    - 환경의 지역(local) 범위를 설정.
    - 환경 내에서 액터들이 배치될 공간 정의.
- **마지막 인자 (`8`)**:
    - 한 줄에 배치할 환경의 개수를 지정.
    - 여러 환경은 2D 그리드 형태로 배치.
- **좌표 공간**:
    - 각 환경은 개별적인 지역(local) 좌표 공간을 가지며, 글로벌 시뮬레이션 공간에 내장됨.

<br/>

### Create Actor

- Isaac Gym에서 **액터(Actor)**는 **GymAsset의 인스턴스**로, 특정 환경에 추가되어야만 사용 가능
- 액터는 시뮬레이션 내에서 물리적으로 상호작용하며, 환경마다 고유의 좌표 공간(local coordinates)을 가짐
- 액터를 환경에 추가하려면 에셋, 포즈, 이름, 기타 세부 정보를 지정해야 함

```python
pose = gymapi.Transform()
pose.p = gymapi.Vec3(0.0, 1.0, 0.0)  # 위치 설정
pose.r = gymapi.Quat(-0.707107, 0.0, 0.0, 0.707107)  # -90도 회전

actor_handle = gym.create_actor(env, asset, pose, "MyActor", 0, 1)
```

- **포즈(Pose)**:
    - **`pose.p`**: 액터의 위치를 나타내는 벡터.
    - **`pose.r`**: 액터의 회전을 나타내는 쿼터니언(quaternion).
    - 쿼터니언은 `(x, y, z, w)` 순서로 지정.
        - 예: `(-0.707107, 0.0, 0.0, 0.707107)`은 x축을 기준으로 -90도 회전을 의미.
- **편의 유틸리티**:
    - 쿼터니언을 직접 계산하지 않고, **축-각도(axis-angle)** 형태로 정의 가능:
        
        ```python
        pose.r = gymapi.Quat.from_axis_angle(gymapi.Vec3(1, 0, 0), -0.5 * math.pi)
        ```
        
- **이름(Name)**:
    - 각 액터는 고유 이름을 가질 수 있음.
    - 이름은 선택 사항이며, 액터를 참조하려면 **핸들(handle)**을 저장하는 것이 효율적.
- **충돌 그룹(Collision Group) 및 필터(Collision Filter)**:
    - **`collision_group`**:
        - 액터가 속한 충돌 그룹을 지정.
        - 동일한 충돌 그룹에 속한 액터끼리만 충돌 가능.
        - 환경별로 충돌 그룹을 다르게 설정해 환경 간 물리적 상호작용 방지 가능.
        - `-1`: 모든 그룹과 충돌하도록 설정.
    - **`collision_filter`**:
        - 충돌을 필터링하는 비트 마스크.
        - 특정 객체 간의 충돌 또는 자기 충돌(self-collision)을 방지 가능.

<br/>

### Initializing Environments and Actors

```python fold

# 환경 생성 매개변수 설정
num_envs = 64
envs_per_row = 8
env_spacing = 2.0
env_lower = gymapi.Vec3(-env_spacing, 0.0, -env_spacing)
env_upper = gymapi.Vec3(env_spacing, env_spacing, env_spacing)

envs = []
actor_handles = []

# 환경 및 액터 생성
for i in range(num_envs):
    env = gym.create_env(sim, env_lower, env_upper, envs_per_row)
    envs.append(env)

    height = random.uniform(1.0, 2.5)  # 액터의 높이 랜덤화

    pose = gymapi.Transform()
    pose.p = gymapi.Vec3(0.0, height, 0.0)

    actor_handle = gym.create_actor(env, asset, pose, "MyActor", i, 1)
    actor_handles.append(actor_handle)
```

- **환경 매개변수**:
    - **`env_spacing`**: 환경 간 간격.
    - **`env_lower`**와 **`env_upper`**: 환경의 로컬 범위를 정의.
- **충돌 그룹**:
    - 각 액터의 충돌 그룹은 환경 인덱스(`i`)로 설정해, 환경 간 물리적 상호작용 방지.
- **핸들 캐싱**:
    - 각 환경과 액터의 핸들을 리스트에 저장해 이후 코드에서 효율적으로 참조.

<br/><br/>

## Running the Simulation

- 환경과 파라미터를 설정한 후, 시뮬레이션은 **루프**를 통해 실행
- 이 루프의 각 반복은 시뮬레이션의 **하나의 시간 단계(time step)**를 나타냄

```python
while True:
    # 물리 계산 실행
    gym.simulate(sim)
    # 계산 결과 동기화
    gym.fetch_results(sim, True)
```

1. **물리 계산 단계**:
    - `gym.simulate(sim)`을 호출하여 물리 시뮬레이션을 실행.
2. **결과 수집**:
    - `gym.fetch_results(sim, True)`로 계산 결과를 동기화.

<br/><br/>

## Adding a Viewer

```python fold

while not gym.query_viewer_has_closed(viewer):

    # 물리 시뮬레이션 단계
    gym.simulate(sim)
    gym.fetch_results(sim, True)

    # 뷰어 업데이트
    gym.step_graphics(sim)
    gym.draw_viewer(viewer, sim, True)

    # 실시간 동기화
    gym.sync_frame_time(sim)
    
gym.destroy_viewer(viewer)
gym.destroy_sim(sim)
```

<br/>

- 기본 설정으로 창이 열리며, **`isaacgym.gymapi.CameraProperties`**를 커스터마이징하여 크기와 기타 속성을 변경 가능.
	
	```python
	cam_props = gymapi.CameraProperties()
	viewer = gym.create_viewer(sim, cam_props)
	```

- 시뮬레이션 루프에서 뷰어를 업데이트하려면 다음 코드를 추가합니다:
	
	```python
	gym.step_graphics(sim)
	gym.draw_viewer(viewer, sim, True)
	```
	
	- **`step_graphics`**: 물리 상태와 시각적 표현을 동기화.
		- **카메라 센서 렌더링**만 필요할 경우 `step_graphics`만 호출.
	- **`draw_viewer`**: 뷰어에 최신 스냅샷을 렌더링.<br/><br/>

- 시뮬레이션이 실시간보다 빠르게 실행될 수 있으므로, 이를 실시간과 동기화하기 위해 다음 코드를 추가
	
	```python
	gym.sync_frame_time(sim)
	```
	
	- 이 코드는 시뮬레이션 속도를 실시간으로 제한
	- 시뮬레이션이 실시간보다 느리게 실행되면 아무 효과 없음<br/><br/>

- 사용자가 뷰어 창을 닫으면 시뮬레이션 루프를 종료하도록 설정 가능
	
	```python
	while not gym.query_viewer_has_closed(viewer):
	    # 시뮬레이션 루프
	```

- 시뮬레이션 종료 시, **뷰어(Viewer)**와 **시뮬레이터(Simulator)** 객체를 해제해야 함
	```python
	gym.destroy_viewer(viewer)
	gym.destroy_sim(sim)
	```

<br/>

```ad-tip
title: Viewer GUI
collapse: true

#### **1.1 Actors 탭**

- **환경(Environment) 및 액터(Actor) 선택**:
    - 특정 환경과 해당 환경의 액터를 선택 가능.
- **하위 탭**:
    1. **Bodies 서브탭**:
        - 선택된 액터의 강체(rigid body) 정보를 표시.
        - 강체의 색상을 변경하거나 축(axes)의 시각화를 토글 가능.
    2. **DOFs 서브탭**:
        - 액터의 자유도(DOF) 정보를 표시.
        - GUI에서 DOF 속성을 편집 가능 (실험적 기능).
    3. **Pose Override 서브탭**:
        - 액터의 포즈를 수동으로 설정 가능.
        - 슬라이더를 사용해 포즈 및 드라이브 목표를 조작.
        - 액터의 자유도를 탐색하거나 조작하는 데 유용.

#### **1.2 Sim 탭**

- **물리 시뮬레이션 파라미터**:
    - PhysX 또는 Flex 시뮬레이션 유형에 따라 다름.
    - 사용자가 해당 파라미터를 수정 가능.

#### **1.3 Viewer 탭**

- **시각화 옵션**:
    - 그래픽 표현(시각적 모델)과 물리적 형태(충돌 모델) 간의 전환.
    - 물리적 동작을 디버깅할 때 유용.

#### **1.4 Perf 탭**

- **시뮬레이션 성능 측정**:
    - 성능 측정을 위한 다양한 지표 제공.
    - 프레임 속도(FPS)를 측정 창(window) 단위로 보고.
- 주요 성능 지표:
    1. **Frame Time**:
        - 한 시뮬레이션 단계가 시작되고 다음 단계가 시작될 때까지 걸린 시간.
    2. **Physics Simulation Time**:
        - 물리 솔버가 실행되는 시간.
    3. **Physics Data Copy Time**:
        - 시뮬레이션 결과를 복사하는 데 소요된 시간.
    4. **Idle Time**:
        - `gym.sync_frame_time(sim)`에서 대기하는 시간.
    5. **Viewer Rendering Time**:
        - 뷰어를 렌더링하고 표시하는 데 소요된 시간.
    6. **Sensor Image Copy Time**:
        - 센서 이미지 데이터를 GPU에서 CPU로 복사하는 시간.
    7. **Sensor Image Rendering Time**:
        - GPU 버퍼에 카메라 센서(뷰어 카메라 제외)를 렌더링하는 데 소요된 시간.
```

<br/><br/>

## Custom Mouse/Keyboard Input

- Isaac Gym 뷰어(Viewer)에서 **마우스/키보드 입력**을 처리하려면 특정 동작 이벤트를 **구독(subscribe)**하고 **쿼리(query)**할 수 있음
	```python
	gym.subscribe_viewer_keyboard_event(viewer, gymapi.KEY_SPACE, "space_shoot")
	gym.subscribe_viewer_keyboard_event(viewer, gymapi.KEY_R, "reset")
	gym.subscribe_viewer_mouse_event(viewer, gymapi.MOUSE_LEFT_BUTTON, "mouse_shoot")
	```
	
	- `gymapi.KEY_SPACE`: **스페이스바** 입력 이벤트 구독.
	- `gymapi.KEY_R`: **R 키** 입력 이벤트 구독.
	- `gymapi.MOUSE_LEFT_BUTTON`: **마우스 왼쪽 버튼** 입력 이벤트 구독.
	- 이벤트 이름(예: `"space_shoot"`, `"reset"`)은 사용자가 정의.<br/><br/>
- **`gym.query_viewer_action_events(viewer)`**: 이벤트를 쿼리하여 현재 발생한 동작을 확인.
	
	```python
	while not gym.query_viewer_has_closed(viewer):
	    # 이벤트 처리 루프
	    for evt in gym.query_viewer_action_events(viewer):
	        if evt.action == "space_shoot":
	            print("Spacebar pressed: Shooting!")
	        elif evt.action == "reset":
	            print("R key pressed: Resetting!")
	        elif evt.action == "mouse_shoot":
	            print("Left mouse button clicked: Shooting!")
	```
	
	- `evt.action`: 구독한 이벤트 이름으로 해당 동작을 식별.