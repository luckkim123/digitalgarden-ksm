---
{"dg-publish":true,"permalink":"/3-archive/30-fleeting-notes/figure/","tags":["Project"]}
---

# Overview
---
### Background


<br/>

### Purpose


<br/>

### Key Objectives

#### Figure
- [x] (a) Imaging Sonar의 Geometry와 (b) Image mechanism을 보여주는 Vertical section view
- [x] (a) Imaging Sonar + 881A geometry (b) 물체가 Horizontal하게 놓여있을 때 + Fusion 결과, (c) 물체가 Horizontal하게 놓여있지 않을 때 Fusion 결과 (xyz 좌표계)
      *이 그림으로 "Horizontal state"를 정의*
- [x] 수조 관련 (a) 사이클롭스 사진 + 디드슨, 881A 어디 부착되어 있는지 표시 (b) 수조 사진 가로세로 표시 (c) 실제 실험 사진
- [ ] 물체 사진 - 가로세로 높이 슬로프각도 표시

<br/>

#### Equation

- [x] $r_{e,min}, r_{e,max}$
- [x] Sonar image로 부터 3D reconstruction 하는 식


<br/><br/>

# Progress
---
##### Reference
- 1.(a)
![3_Archive/31_Attachments/Pasted image 20240716152838.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240716152838.png)![3_Archive/31_Attachments/Pasted image 20240716153042.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240716153042.png)
- 1.(b)
![3_Archive/31_Attachments/Pasted image 20240716152855.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240716152855.png)![3_Archive/31_Attachments/Pasted image 20240716153054.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240716153054.png)

- 2(a)
	![3_Archive/31_Attachments/Pasted image 20240717162509.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240717162509.png)![3_Archive/31_Attachments/Pasted image 20240717162531.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240717162531.png)

- Spec
  ![3_Archive/31_Attachments/Pasted image 20240718135608.png|+grid](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240718135608.png)
#### Figure


#### Equation

```tex
\documentclass{article}
\usepackage{graphicx} % Required for inserting images
\usepackage{amsmath}
\begin{document}

\section{equation}
\subsection{equation 1}

\begin{equation}
    r_{emin}=\frac{H}{\sin(t+\frac{\theta_{cp}}{2})}
\end{equation}
\begin{equation}
    r_{emax}=\frac{H}{\sin(t-\frac{\theta_{cp}}{2})}
\end{equation}

\subsection{equation 2}
\begin{equation}
    \begin{bmatrix}
        X_{cp}^{Local}(j) \\\\ Y_{cp}^{Loca}l(j) \\\\ Z_{cp}^{Local}(j)
    \end{bmatrix}
    = \begin{bmatrix}
        r_{cp}(j)\cos{(\Phi_{cp}(j))}\cos{(t+\frac{\theta_{cp}}{2})} \\\\
        r_{cp}(j)\sin(\Phi_{cp}(j)) \\\\
        r_{cp}(j)\cos(\Phi_{cp}(j))\sin(t+\frac{\theta_{cp}}{2})
    \end{bmatrix}
\end{equation}

\end{document}
```

![3_Archive/31_Attachments/Pasted image 20240716152559.png](/img/user/3_Archive/31_Attachments/Pasted%20image%2020240716152559.png)

<br/><br/>

# Resource
---

