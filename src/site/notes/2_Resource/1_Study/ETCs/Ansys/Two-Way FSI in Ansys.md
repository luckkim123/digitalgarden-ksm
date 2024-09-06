---
{"dg-publish":true,"permalink":"/2-resource/1-study/et-cs/ansys/two-way-fsi-in-ansys/","noteIcon":"","created":"2024-09-04"}
---

# One-Way FSI
## 3D Modeling Tools
- FSI 해석을 위해 필요한 물체의 3D modeling
  CAD, Cartia, Solid Works 혹은 Ansys SpaceClaim 등 3D modeling tools를 사용
>[!info] 지원 포맷
>![3_Archive/1_Attachments/Pasted image 20240904202908.png|500](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904202908.png)![3_Archive/1_Attachments/스크린샷 2024-09-04 203008.png|500](/img/user/3_Archive/1_Attachments/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-09-04%20203008.png)

<br>

## Ansys
### Fluid Flow (Fluent)
#### Ansys Workbench에 Fluent 추가 및 3D model 불러오기
- Ansys workbench 좌측 `Toolbox`에 있는 **Fluid Flow(Fluent)** tool을 `Project Schematic`에 드래그로 추가
- Fluent의 Geometry에서 3D model 데이터 Import
>[!info] Ansys Workbench
>![3_Archive/1_Attachments/Pasted image 20240904203627.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904203627.png)


<br>

#### Geometry
- SpaceClaim, DesignModeler, Discovery 중 아무거나 사용 가능 (여기서는 SpaceClaim 사용)

- 여러개의 Component로 구성된 모델을 하나로 통합
>[!info] Combine
>![3_Archive/1_Attachments/Pasted image 20240904204111.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904204111.png)

- 3D model에 이상이 없는지 확인
>[!info] Check Geometry
>![3_Archive/1_Attachments/Pasted image 20240904213231.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904213231.png)
  
- Fluid domain 생성
  Fluid domain은 `Enclousre`로 생성하는데, 이때 Inlet과 Outlet 영역을 제외한 면은 모두 Wall로 설정되기 때문에, 벽면의 마찰력으로 인한 유체의 유동이 물체의 유체 역학 해석에 영향을 미치지 않도록 충분히 크게 설정 
  >[!info] Enclosure
  >![3_Archive/1_Attachments/Pasted image 20240904213714.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904213714.png)![3_Archive/1_Attachments/Pasted image 20240904214053.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904214053.png)
  
  >[!info] Set units
  >![3_Archive/1_Attachments/Pasted image 20240904213928.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904213928.png)![3_Archive/1_Attachments/Pasted image 20240904213952.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904213952.png)

- Namespace 생성
  Inlet, outlet, [[3_Archive/ETCs/Annotations/walls\|walls]], [[3_Archive/ETCs/Annotations/walls-fluid-solid\|walls-fluid-solid]], [[3_Archive/ETCs/Annotations/walls-solid-fluid\|walls-solid-fluid]] 등을 생성
  >[!info] Create NS
  >![3_Archive/1_Attachments/Pasted image 20240904214927.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904214927.png)

<br>

#### Mesh
- Fluid Flow(Fluent)에서 `Mesh` ▶ `Edit`
>[!info] Editing mesh
>![3_Archive/1_Attachments/Pasted image 20240904215214.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904215214.png)![3_Archive/1_Attachments/Pasted image 20240904220451.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904220451.png)

- [[3_Archive/ETCs/Annotations/Inflation\|Inflation]] 추가
  Scope 에는 Fluid domain인 Enclosure를 선택하고, Definition boundary에는 `wall-fluid-solid` 선택
>[!info] Insert inflation
>
>![3_Archive/1_Attachments/Pasted image 20240904221046.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904221046.png)![3_Archive/1_Attachments/Pasted image 20240904221229.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904221229.png)
>![3_Archive/1_Attachments/Pasted image 20240904221718.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904221718.png)

- Mesh 생성
>[!info] Mesh generation
>![3_Archive/1_Attachments/Pasted image 20240904221446.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904221446.png)![3_Archive/1_Attachments/Pasted image 20240904221508.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904221508.png)<br>
>
>- Mesh size를 조절하고 싶을 경우
>  ![3_Archive/1_Attachments/Pasted image 20240904222519.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904222519.png)

- Workbench ▶ Fluent ▶ `Mesh` ▶ `Update`
>[!info] Update the mesh
>![3_Archive/1_Attachments/Pasted image 20240904222838.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904222838.png)

<br>

#### Setup
- Workbench ▶ Fluent ▶ `Setup` ▶ `Edit`
>[!info] Setup
>![3_Archive/1_Attachments/Pasted image 20240904222933.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904222933.png)![3_Archive/1_Attachments/Pasted image 20240904222942.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904222942.png)
>![3_Archive/1_Attachments/Pasted image 20240904223029.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904223029.png)

- Materials에 `water-liquid` 추가
  `Materials` ▶ `Fluid` ▶ `air` (Double click) ▶ `Fluent Database...`
>[!info] Create/Edit Materials
>![3_Archive/1_Attachments/Pasted image 20240904223430.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904223430.png)
>![3_Archive/1_Attachments/Pasted image 20240904223446.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904223446.png)![3_Archive/1_Attachments/Pasted image 20240904223521.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904223521.png)

- Fluid의 종류 변경
  `Cell Zone Conditions` ▶ `Fluid` ▶ `enclosure_enclosure`
>[!info] Fluid
>![3_Archive/1_Attachments/Pasted image 20240904223700.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904223700.png)

- Boundary conditions 설정
  `Boundary Conditions` ▶ `Inlet`
>[!info] Velocity Inlet
>![3_Archive/1_Attachments/Pasted image 20240904231455.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904231455.png)

- Report definitions 설정
  `Solution` ▶ `Report Definitions` ▶ `New`
>[!info] Report Definition
>![3_Archive/1_Attachments/Pasted image 20240904224854.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904224854.png)![3_Archive/1_Attachments/Pasted image 20240904225100.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904225100.png)


- Initialization
  `Solution` ▶ `Initialization`
>[!info] Solution Initialization
>![3_Archive/1_Attachments/Pasted image 20240904225217.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904225217.png)

- Run calculation
  `Solution` ▶  `Run Calculation`
>[!info] Run Calculation
>![3_Archive/1_Attachments/Pasted image 20240904225540.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904225540.png)![3_Archive/1_Attachments/Pasted image 20240904232654.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904232654.png)

- 결과 확인
  `Results` ▶ `Create` ▶ `Plane`
  `Results` ▶ `Contours` ▶ `New`
>[!info] Create Contours
>![3_Archive/1_Attachments/Pasted image 20240904230132.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904230132.png)![3_Archive/1_Attachments/Pasted image 20240904230143.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904230143.png)
>![3_Archive/1_Attachments/Pasted image 20240904233040.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904233040.png)![3_Archive/1_Attachments/Pasted image 20240904233059.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240904233059.png)
>![3_Archive/1_Attachments/제목 없는 동영상 2.gif](/img/user/3_Archive/1_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%202.gif)


<br><br>

### Static Structural
#### Ansys Workbench에 Static Structural 추가 및 Fluent와 연결
- Workbench 좌측 Toolbox에서 `Static Structural`를 Project Schematic에 추가
- `Geometry` 끼리 연결 및 Fluent의 `Solution`과 Static Structural의 `Setup` 연결
>[!info] Project Schematic
>![3_Archive/1_Attachments/Pasted image 20240905105237.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905105237.png)

#### Model
- `Static Structural` ▶ `Model` ▶ `Edit`
>[!info] Editing model
>![3_Archive/1_Attachments/Pasted image 20240905111206.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905111206.png)![3_Archive/1_Attachments/Pasted image 20240905111223.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905111223.png)

- Suppress fluid domain
  `Model` ▶ `Geometry` ▶ Select `Fluid domain` ▶ `Suppress Body`
>[!info] Suppress body
>![3_Archive/1_Attachments/Pasted image 20240905111435.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905111435.png)

- Generate mesh
  Outline에서 Mesh를 클릭하면 좌측 하단에 Mesh에 대한 상세 정보가 뜨며, `Sizing` ▶ `Span Angle Center`에서 Mesh quality를 선택할 수 있음
>[!info] Span Angle Center
>![3_Archive/1_Attachments/Pasted image 20240905111824.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905111824.png)![3_Archive/1_Attachments/Pasted image 20240905111928.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905111928.png)

- Material 선택
  `Model` ▶ `Geometry` ▶ Select `Solid` ▶ `Details of "Solid"` ▶ `Material` ▶ `Assignment`
>[!info] Material
>![3_Archive/1_Attachments/Pasted image 20240905112119.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905112119.png)

- Fixed Support 선택
  본 예제에서는 Hero wings의 Center link가 Cyclops에 부착되어 고정되어 있기 때문에 Center link를 Fixed Support로 선택
  `Static Structural` ▶ `Insert` ▶ `Fixed Support`
>[!info] Fixed Support
>![3_Archive/1_Attachments/Pasted image 20240905112610.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905112610.png)![3_Archive/1_Attachments/Pasted image 20240905112726.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905112726.png)

- Imported Pressure 선택
  `Static Structural` ▶ `Imported Load` ▶ `Insert` ▶ `Pressure` ▶ Select Named Selection `wall-solid-fluid`
>[!info] Imported Pressure
>![3_Archive/1_Attachments/Pasted image 20240905113007.png|300](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905113007.png)

- Solution 종류 선택
  `Static Structural` ▶ `Solution` ▶ `Insert` ▶ Select type of solutions what you want to analysis
>[!info] Solution
>![3_Archive/1_Attachments/Pasted image 20240905113428.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905113428.png)![Pasted image 20240905203723.png|+grid](/img/user/3_Archive/1_Attachments/Pasted%20image%2020240905203723.png)

- Solve
>[!info] Results
>![제목 없는 동영상 (1) 2.gif](/img/user/3_Archive/1_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(1)%202.gif)![제목 없는 동영상 (2) 2.gif](/img/user/3_Archive/1_Attachments/%EC%A0%9C%EB%AA%A9%20%EC%97%86%EB%8A%94%20%EB%8F%99%EC%98%81%EC%83%81%20(2)%202.gif)

