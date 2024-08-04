---
{"dg-publish":true,"permalink":"/0-project/00-research-internship/001-3-d-reconstruction/time-synchronizing/","tags":["Project","Project/Stereo2PCD"],"noteIcon":"","created":"2024-07-09"}
---

- [Evernote](https://www.evernote.com/shard/s515/sh/07e72a43-ebf0-bcdb-9998-539d9d9df5c7/h1JE9gPgLl1KRIXs1mTqPr9IzYUACmdIqTy34fD4-e4-gg-F8pcNufh8DQ)
# Overview
#### Purpose
- Stereo 카메라 데이터의 촬영 시간을 동기화(Time synchronizing)하여 추후 Calibration 및 Reconstruction 에 용이하게 함

#### Background
- 실험 데이터를 취득할 때 GoPro 를 정확하게 동시에 시작하지 않았기 때문에 시간 동기화가 필요

#### Key Objectives
- 이미지의 촬영 시간을 기준으로 좌우 카메라 데이터를 시간 동기화 한 뒤, 별도 폴더에 저장

![3_Archive/31_Attachments/G0034391.jpg|500](/img/user/3_Archive/31_Attachments/G0034391.jpg)

---
# Progress

- PIL 패키지의 `ExifTags.TAGS` 를 사용하여 이미지의 메타 데이터를 추출한 뒤 촬영 시간 정보 추출
#### Issues
- 좌우 고프로의 시간이 초기화되어 있지 않아 메타 데이터 상 촬영 시간이 하루 이상 차이가 나기 때문에 해당 정보로 시간 동기화를 할 수 없음

##### Solutions
- 좌우 고프로에 촬영된 휴대폰 타이머를 참고하여 각 프레임의 촬영 시간을 계산한 뒤 시간 동기화 수행

![3_Archive/31_Attachments/Screenshot from 2024-07-01 13-42-45.png](/img/user/3_Archive/31_Attachments/Screenshot%20from%202024-07-01%2013-42-45.png)

---
# Resource

- [[1_Area/11_Study/111_Coding/Python/Python - 이미지 메타정보(EXIF)로 촬영일시 찾기\|Python - 이미지 메타정보(EXIF)로 촬영일시 찾기]]

