---
{"dg-publish":true,"permalink":"/1-area/10-paper-review/csp-net/experiments/ablation-studies/","tags":["PaperReview","PaperReview/Backbone/CSPNet"],"noteIcon":"","created":"2024-03-12, 19:29"}
---

```ad-tip
title: Implementation Details
collapse: true
###### Dataset
- Dataset: 
- Training / Validation / Test set: 
- Data augmentation: 
- Pre-processing: 

---
###### Training
- Optimization: 
- Batch size: 
- Epoch: 
- Learning strategy:
	- Learning rate: 
	- Learning rate scheduler: 
- Momentum & Weight decay: 
- ETC:
	- 

---
###### Evaluation
- 

```
---
## Computational Bottleneck
![2_Resource/20_Zotero/201_Literature Notes/@WangEtAl2019/image-11-x83-y558.png](/img/user/2_Resource/20_Zotero/201_Literature%20Notes/@WangEtAl2019/image-11-x83-y558.png)

---
### Analysis
- PeleeNet-YOLO: Head 가 Feature pyramid 를 통합할 때 Computational bottleneck 발생
- PeleeNet-PRN: PeleeNet backbone 의 Transition layers 에서 Computational bottleneck 발생
- CSPPeleeNet-EFM: 모든 Computational bottleneck 현상이 균형을 맞추고 있으며, 앞선 모델보다 각 80%, 44% 감소
---
```ad-tip
title: Implementation Details
collapse: true
###### Dataset
- Dataset: 
- Training / Validation / Test set: 
- Data augmentation: 
- Pre-processing: 

---
###### Training
- Optimization: 
- Batch size: 
- Epoch: 
- Learning strategy:
	- Learning rate: 
	- Learning rate scheduler: 
- Momentum & Weight decay: 
- ETC:
	- 

---
###### Evaluation
- 

```
---
## Memory Traffic
![2_Resource/20_Zotero/201_Literature Notes/@WangEtAl2019/image-11-x121-y224.png](/img/user/2_Resource/20_Zotero/201_Literature%20Notes/@WangEtAl2019/image-11-x121-y224.png)

---
### Analysis
- CSPResNeXt50 의 CIO (32.6 M) 는 ResNeXt50 (34.4 M) 보다 낮음
- 또한, CSPResNeXt50 은 ResXBlock 의 Bottleneck layers 를 제거하여도, 입 출력 Feature map 의 Channel 을 동일하게 유지
	- 이를 통해 FLOPs 가 고정될 때 MAC 가 가장 낮아지고 연산이 효율적으로 됨

>CSPResNeXt50 은 작은 CIO 와 FLOPs 를 보여주며, Computation 측면에서 ResNeXt50 보다 22% 더 우수한 성능을 보여줌
---
```ad-tip
title: Implementation Details
collapse: true
###### Dataset
- Dataset: 
- Training / Validation / Test set: 
- Data augmentation: 
- Pre-processing: 

---
###### Training
- Optimization: 
- Batch size: 
- Epoch: 
- Learning strategy:
	- Learning rate: 
	- Learning rate scheduler: 
- Momentum & Weight decay: 
- ETC:
	- 

---
###### Evaluation
- 

```
---
## Inference Rate
- 제안하는 방법을 mobile GPU(NVIDIA Jetson TX2)와 CPU(Intel Core i9-9900K)에서 실험
- CPU 에서 Inference rate 는 OpenCV DNN 모듈로 검증
- 공평한 비교를 위해 Model compression 혹은 Quantization 은 추가하지 않음

![2_Resource/20_Zotero/201_Literature Notes/@WangEtAl2019/image-12-x184-y549.png|500](/img/user/2_Resource/20_Zotero/201_Literature%20Notes/@WangEtAl2019/image-12-x184-y549.png)

---
### Analysis
- AP$_{50}$ 은 CSPPeleeNet reference, EFM-SAM 이 44.6% 로 가장 높음
- GPU, CPU, mGPU 의 경우 CSPDenseNet reference, PRN 이 400, 102, 73 FPS 로 가장 빠름
---
