---
{"dg-publish":true,"permalink":"/0-project/pkrc/pkrc-3-d-visualization-of-profiling-sonar-881-a/","tags":["Project","Project/PKRC"],"noteIcon":"","created":"2024-12-09"}
---

# Overview

```ad-note
title: **Background**
- PKRC 과제 (뻘제거 로봇 개발)
	- 수중에서는 GPS를 사용할 수 없기 때문에 로봇의 위치를 인식하는 데 어려움이 있음
	- 로봇의 위치를 인식하기 위해 수면 위에 LiDAR와 SONAR 센서를 부착한 수상선을 띄우고, 해당 수상선에서 LiDAR를 사용하여 global localization을 수행하며, SONAR에서 로봇을 관측하여 localization 수행<br/><br/>
- 현황
	- LiDAR를 사용하는 SLAM 알고리즘 구동 테스트 완료
	- 현재는 연구실에 있는 Profiling SONAR (Imagenex 881A)를 사용하여 feasibility test 수행
	- 881A 데이터는 정상적으로 나오는 것을 확인하였으며, 추후 localization 알고리즘 개발을 위해 1-D 데이터를 3-D 로 시각화할 필요가 있음
```

```ad-abstract
title: **Purpose**
- 881A 데이터를 ROS 상에서 topic 형태로 송수신이 가능하도록 하며, 1-D 데이터를 RViz 상에서 3-D로 시각화하는 코드 작성
```

```ad-example
title: **Key Objectives**
- [x] Cyclops 내부에서 881A ROS 코드 파악
- [ ] 881A의 ROS msg 포맷 분석
	- RViz에서 인식 가능한 `visualization_msgs/Marker` msg 형식으로 변환하기 위해 ROS msg에 어떤 데이터를 포함하고 있는지 분석
- [x] 881A를 사용하여 실험용 데이터를 Bagging
- [ ] 881A의 1-D data를 3-D로 변환하기 위한 알고리즘 분석
- [ ] 881A 데이터를 3-D로 변환하여 `visualization_msgs/Marker` msg 형식으로 변환 및 publish하는 ROS node 작성
```

<br/><br/>

# Progress
## Code 분석
- `catkin_ws/src/ros_881a/src/ros_881a.cpp`
	```cpp fold
	int main(int argc, char **argv)
	{
		ros::init(argc, argv, "ros_881A");
	
		ros::NodeHandle nh;
		
		// ROS 퍼블리셔를 선언
		ros::Publisher pub881A = nh.advertise<std_msgs::String>("/ros_881A/data", 1000);
		ros::Publisher pubd881A = nh.advertise<std_msgs::Int64MultiArray>("/ros_881A/ndata", 1000);
	
		// 메시지 객체 선언
		std_msgs::String msg881A;
		DataPacket_881A packet881A;
		std_msgs::Int64MultiArray d881A;
	
		d881A.data.clear();
		ros::Rate loop_rate(10);
		std::cout << ros::ok() << std::endl;
	
		// ROS 루프
		while (ros::ok()) {
			// 센서 초기화 명령 수행
			c881A->initCmd();
			usleep(100000);
			
			// 센서 데이터 요청
			c881A->RequestData();
	
			// 데이터 패킷 생성 및 데이터 획득
			packet881A.identifier = 1;
			packet881A.sensor881A = c881A->GetData();
			packet881A.cmd881A = c881A->GetCmdInfo();
	
			// 데이터를 문자열 스트림에 추가
			std::stringstream ss881A;
			ss881A << static_cast<int>(packet881A.sensor881A.Range) << ",";
			ss881A << static_cast<int>(packet881A.cmd881A.StartGain) << ",";
			ss881A << packet881A.cmd881A.SectorWidth * 3 << ",";
			ss881A << packet881A.cmd881A.TrainAngle * 3 - 180 << ",";
			ss881A << packet881A.sensor881A.HeadPosition << ",";
			ss881A << packet881A.sensor881A.ProfileRange << ",";
			
			// 첫 번째 Echo 데이터 처리
			ss881A << static_cast<int>(packet881A.sensor881A.Echo[0]);
			d881A.data.push_back(static_cast<int>(packet881A.sensor881A.Echo[0]));
			
			// 나머지 Echo 데이터를 반복적으로 추가
			for (int i = 0; i < 500; i++) {
				ss881A << "," << static_cast<int>(packet881A.sensor881A.Echo[i]);
				d881A.data.push_back(static_cast<int>(packet881A.sensor881A.Echo[i]));
			}
			
			// String 메시지에 문자열 데이터 저장
			msg881A.data = ss881A.str();
	
			pub881A.publish(msg881A);
			pubd881A.publish(d881A);
	
			d881A.data.clear();
			ros::spinOnce();
			loop_rate.sleep();
		}
	}
	
	```

<br/>

- `catkin_ws/src/ros_881a/src/ros_881a.h`
	```cpp fold
	typedef struct _Cmd_881A
	{
		BYTE init_0xFE;
		BYTE init_0x44;
		BYTE HeadID;
		BYTE Range;
		BYTE Reserved1;
		BYTE Rev_Hold;
		BYTE Master_Slave;
		BYTE Reserved2;
		BYTE StartGain;
		BYTE LOGF;
		BYTE Absorption;
		BYTE TrainAngle;
		BYTE SectorWidth;
		BYTE StepSize;
		BYTE PulseLength;
		BYTE ProfileMinRange;
		BYTE Reserved3;
		BYTE Reserved4;
		BYTE Reserved5;
		BYTE DataPoints;
		BYTE DataBits;
		BYTE UpBaud;
		BYTE Profile;
		BYTE Calibrate;
		BYTE SwitchDelay;
		BYTE frequency;
		BYTE term_0xFD;
	
	}Cmd_881A;
	
	
	typedef struct _Sensor_881A
	{
		//BYTE identifier;
		BYTE RawData[513];//RawData[513]
		BYTE ASCII[3];//ASCII[3]
		BYTE HeadID;
		BYTE SerialStatus;
		short HeadPosition;
		BYTE Range;
		short ProfileRange;
		WORD DataBytes;
		BYTE Echo[500];
		BYTE TerminationByte;
	
	}Sensor_881A;
	
	
	typedef struct _Packet_881A
	{
		BYTE identifier;
		Cmd_881A cmd881A;
		Sensor_881A sensor881A;
	}DataPacket_881A;
	```

<br/><br/>

## visualization_msgs/Marker message

- Reference: https://wiki.ros.org/rviz/DisplayTypes/Marker

	```plain fold
	uint8 ARROW=0
	uint8 CUBE=1
	uint8 SPHERE=2
	uint8 CYLINDER=3
	uint8 LINE_STRIP=4
	uint8 LINE_LIST=5
	uint8 CUBE_LIST=6
	uint8 SPHERE_LIST=7
	uint8 POINTS=8
	uint8 TEXT_VIEW_FACING=9
	uint8 MESH_RESOURCE=10
	uint8 TRIANGLE_LIST=11
	
	uint8 ADD=0
	uint8 MODIFY=0
	uint8 DELETE=2
	uint8 DELETEALL=3
	
	Header header                        # header for time/frame information
	string ns                            # Namespace to place this object in... used in conjunction with id to create a unique name for the object
	int32 id                           # object ID useful in conjunction with the namespace for manipulating and deleting the object later
	int32 type                         # Type of object
	int32 action                         # 0 add/modify an object, 1 (deprecated), 2 deletes an object, 3 deletes all objects
	geometry_msgs/Pose pose                 # Pose of the object
	geometry_msgs/Vector3 scale             # Scale of the object 1,1,1 means default (usually 1 meter square)
	std_msgs/ColorRGBA color             # Color [0.0-1.0]
	duration lifetime                    # How long the object should last before being automatically deleted.  0 means forever
	bool frame_locked                    # If this marker should be frame-locked, i.e. retransformed into its frame every timestep
	
	#Only used if the type specified has some use for them (eg. POINTS, LINE_STRIP, ...)
	#number of colors must either be 0 or equal to the number of points
	geometry_msgs/Point[] points
	
	#NOTE: alpha is not yet used
	std_msgs/ColorRGBA[] colors
	
	# NOTE: only used for text markers
	string text
	
	# NOTE: only used for MESH_RESOURCE markers
	string mesh_resource
	bool mesh_use_embedded_materials
	```

<br/><br/>

## ROS Bag
- 수상선의 Jetson Orin에 ros_881a 패키지를 빌드하고, `{bash} rosrun ros_881a ros_881a` 로 881A 동작
- 결과 `ros_881a/data`, `ros_881a/ndata` 모두 정상적으로 publish 되었으며, ROS bagging 수행하였음
- NAS: `/2024/2024_연구관련 프로그램 및 코드/04_김승민/2024-12-09-15-36-15.bag`
# Resource

