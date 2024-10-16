---
{"dg-publish":true,"permalink":"/3-archive/et-cs/conference-materials/survey-of-sonar/","noteIcon":"","created":"2024-10-17"}
---

```ad-tip
title: Sonar 조건

- **ROS화 가능성**.
- SONAR 간섭 여부 확인.
- 가격 및 납기일.
- **사이즈 및 무게**.
```

## BlueRobotics
- [Sonoptix ECHO Multibeam Imaging Sonar](https://bluerobotics.com/store/sonars/imaging-sonars/sonoptix-echo/)
	- ![[Sonoptix_ECHO_Datasheet.pdf]]
	- Price: $ 9,000
	- ROS: [Official (expired)](https://github.com/bluerobotics/bluerov-ros-pkg)
	- Frequency: 400 kHz (>30m) / 700 kHz (<30m)
	- Range: 100 m @ 400 kHz / 30 m @ 700 kHz
	- Size: 149.7 x 100.0 x 42.3
	- Weight: 0.75 kg

<br>

## WaterLinked
- [Sonar 3D-15](https://waterlinked.com/3dsonar/sonar-3d-15)
	- [[Datasheet-Sonar-3D-15-RGB-v2.pdf]]
	- Price: $ 27,900
	- ROS: -
	- Frequency: 1.2 MHz (Navigation mode) / 2.4 MHz (Inspection mode)
	- Range: 15 m (Navigation mode) / 4 m (Inspection mode)
	- Size: 120 x 80 x 40
	- Weight: 0.66 kg (Air) / 0.39 kg (Water)

<br>

## TELEDYNE MARINE
![Pasted image 20241017042426.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241017042426.png)

- Site: [Forward Looking Sonars Systems...](https://www.teledynemarine.com/products/product-line/sonar/forward-looking-imaging-sonars)
- ROS: 
	- [Thirdparty - Remote Cocean Systems Pan&Tilt Driver](https://github.com/oceansystemslab/bvt_pantilt)
	- [Thirdparty - Zeabus_imaging_sonar](https://github.com/oceansystemslab/bvt_pantilt)

<br>

## Blueprint Subsea
![Pasted image 20241017042855.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241017042855.png)

- Site: [Blueprint Subsea | Oculus](https://www.blueprintsubsea.com/oculus/)

- Oculus M-Series
	- [[DA-148-P01443-08.pdf]]
	- Price: -
	- ROS: 
		- [Thirdparty - Oculus sonar ROS1](https://github.com/ENSTABretagneRobotics/oculus_ros?tab=readme-ov-file)
		- [Thirdparty - Oculus Driver](https://github.com/ENSTABretagneRobotics/oculus_ros?tab=readme-ov-file)
	- Frequency: 375 kHz
	- Range: 200 m
	- Size: 124 x 122 x 62
	- Weight: 0.98 kg (Air) / 0.36 kg (Water)

<br>

## Cerulean Sonar
- [Omniscan 450 FS](https://ceruleansonar.com/products/omniscan-450?variant=40179023806530)
	- [[Pasted image 20241017043636.png]]
	- Price:
		- 100 m rated: $ 2,295
		- 300 m rated: $ 2,750
	- ROS: - 
		- Docker: [Docker | Cerulean Sonar Docs](https://docs.ceruleansonar.com/c/sonarview/installation/docker)
	- Frequency: 450 kHz
	- Range: 100 m
	- Size: 56 x 67 x 200
	- Weight: 
		- 100 m rated: 0.44 kg (Air) / -0.06 kg (Water)
		- 300 m rated: 0.825 kg (Air) / 0.325 kg (Water)

<br>

## NORBIT
![Pasted image 20241017044103.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241017044103.png)

- Site: [Products & Solutions - NORBIT](https://norbit.com/subsea/products/)
- ROS: [Thirdparty - ROS Norbit Multibeam sonar driver](https://github.com/uri-ocean-robotics/norbit)

- FLS Wide
	- [[PS-150004-8_WBMS-FLS-wide_Pn_12002-AAGDA4_A4-1-1.pdf]]
	- Frequency: 400kHz +/- 40kHz
	- Range: > 250m (NOMINAL 100m) @ 400kHz
	- Size: 236 x 154 x 98
	- Weight: 2.9 kg (Air) / 1.3 kg (Water)

- FLS Compact
	- [[PS-080001-25_WBMS-FLS-Compact_A4.pdf]]
	- Frequency: 400kHz +/- 40kHz
	- Range:250m (NOMINAL 100m) @ 400kHz
	- Size: 236 x 155 x 70
	- Weight: 2.5 kg (Air) / 0.2 kg (Water)

<br>

## IMAGENEX
- [965A 1100 Multibeam Imaging](https://imagenex.com/products/965a-1100-multibeam-imaging)
	- [[965A_1.1_MHz_Imaging_Specs_rev2.pdf]]
	- Price: - 
	- ROS: - 
	- Frequency: 1.1 MHz
	- Range: -
	- Size: 264.8 x 101.6 x 92.1
	- Weight: 1.5 kg (Air) / 0.045 kg (Water)

<br>

## IMPACT SUBSEA
- ISS360 Compact
	- [[ISS360-Compact-Imaging-Sonar-Datasheet-Rev-2.1_compressed.pdf]]
	- Price: -
	- ROS: -
	- Frequency: 700 kHz
	- Range: 90 m
	- Size: 108.5 x 47 x 45
	- Weight: 0.38 kg (Air) / 0.3 kg (Water)

- ISS360HD
	- [[ISS360HD-Imaging-Sonar-Datasheet-Rev-1.4-compressed.pdf]]
	- Price: - 
	- ROS: - 
	- Frequency: 750 kHz
	- Range: 100 m
	- Size: 123.5 x 114 x 114
	- Weight : 0.76 kg (Air) / 0.3 kg (Water)

<br>

## Tritech
- Site: [Multibeam Sonars - Tritech](https://www.tritech.co.uk/products/multibeam-sonars)
- [Gemini 1200is](https://www.tritech.co.uk/products/gemini-1200is)
	- [[1200is_Datasheet_0703-SOM-00003-01.pdf]]
	- Price: -
	- ROS: -
	- Frequency: 720 kHz (Low freq. mode) / 1200 kHz (High freq. mode)
	- Range: 0.1 m - 120 m (Low freq. mode) / 0.1 m - 50 m (High freq. mode)
	- Size: 271 x 135 x 107
	- Weight: 5.0 kg (Air) / 3.0 kg (Water)
