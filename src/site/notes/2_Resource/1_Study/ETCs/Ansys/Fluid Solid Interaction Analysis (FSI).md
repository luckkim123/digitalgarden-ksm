---
{"dg-publish":true,"permalink":"/2-resource/1-study/et-cs/ansys/fluid-solid-interaction-analysis-fsi/","tags":["Project/HeroWings","Study/Ansys/FSI"],"noteIcon":"","created":"2024-09-02"}
---

# Fluid Solid Interaction Analysis - FSI
- Fluid-Solid Interaction (FSI, 유체-구조 상호작용) 분석은 유체와 고체가 상호작용하는 시스템을 분석하는 방법
- 유체의 흐름과 그에 따른 고체의 변형 및 운동을 동시에 고려하여, 유체와 구조물이 서로 영향을 주고받는 복잡한 상호작용을 분석
- FSI 분석에는 유체와 고체간의 상호작용을 처리하는 방식으로 One-way coupling과 Two-way coupling로 구분됨

<br>

## One-Way Coupling
- 단방향 결합
  ==유체에서 고체로만 힘이 전달==되고, 고체가 유체에 미치는 영향을 고려하지 않는 방식
- 유체역학의 해석 결과(속도, 압력 등)가 고체에 적용되지만, 고체의 변형이나 이동은 유체 해석에 다시 반영되지 않음
- 계산이 상대적으로 단순하며, 빠르게 처리할 수 있음
	- 주로 고체의 변형이 미미해서 유체 흐름에 거의 영향을 미치지 않는 경우에 사용됨

<br>

## Two-Way Coup
- 양방향 결합
  ==유체와 고체가 상호 영향을 주는 방식==
- 유체가 고체에 힘을 가해 변형을 일으키면, 변형된 고체는 다시 유체의 흐름을 바꾸고, 바뀐 유체 흐름이 다시 고체에 영향을 미치는 방식으로 ==상호작용이 양방향으로 진행==
- 계산 과정이 복잡하며, 해석 시간이 오래 걸리지만, 유체와 고체의 상호작용을 더 정확하게 반영
	- 물 속의 구조물이 심하게 흔들리는 등, 고체의 변형이 유체 흐름에 큰 영향을 미치는 경우 사용

<br>

| 구분          | One-Way Coupling           | Two-Way Coupling                    |
| ----------- | -------------------------- | ----------------------------------- |
| **상호작용 방향** | 유체가 고체에만 영향을 줌             | 유체와 고체가 상호 영향을 주고받음                 |
| **계산 복잡성**  | 상대적으로 단순하고 계산 시간이 짧음       | 매우 복잡하고 계산 시간이 오래 걸림                |
| **정확도**     | 고체 변형이 유체에 영향을 미치지 않을 때 적합 | 고체 변형이 유체에 영향을 미칠 때 필수              |
| **적용 사례**   | 날개나 건물 표면에 작용하는 바람의 힘 계산 등 | 혈관 내 혈류와 벽의 상호작용, 유체 흐름과 선체의 상호작용 등 |