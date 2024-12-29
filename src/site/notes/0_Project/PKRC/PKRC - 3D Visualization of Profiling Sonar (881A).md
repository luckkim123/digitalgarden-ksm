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
- [x] 881A의 ROS msg 포맷 분석
	- RViz에서 인식 가능한 msg 형식으로 변환하기 위해 ROS msg에 어떤 데이터를 포함하고 있는지 분석
	- Range, SectorWidth, TrainAngle, HeadPosition, ProfileRange 변수 의미 파악
- [x] 881A를 사용하여 실험용 데이터를 Bagging
- [x] 881A 데이터를 3-D로 변환하여 publish하는 ROS node 작성
	- 881A 센서로 부터 얻어진 1D 데이터에서 각 픽셀의 Index를 센서와 반사 지점 사이의 실제 거리로 변환
	- 극 좌표계를 직교 좌표계로 변환한 후 센서의 position과 orientation 정보를 사용하여 센서 기준 좌표계에서 global 좌표계로 변환
- [x] 881A 수조 실험
	- [x] LiDAR의 위치 인식을 통해 구한 위치 좌표로 881A의 센서 좌표 이동
	- [x] LiDAR 및 881A 코드 통합
	- [x] 수조 실험 수행
```

<br/><br/>

# Progress
## Code 분석
- NAS: `연구관련 프로그램 및 코드/PKRC/Codes/ros_881a`<br/><br/>
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

## Data

[[881A_v301_Manual.pdf]]

![Pasted image 20241210154928.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241210154928.png)

- SONAR return data
	![Pasted image 20241210151816.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241210151816.png)
	- Head position
		- 0 to 1200 (-180 to +180 Degrees) in 0.3 degree steps
		- Angle calculation
			- Head angle = 0.3 * (Head pos - 600)
		- Sector width가 45 degrees, train angle이 0 degree 로 되어있기 때문에 head position은 -22.8 ~ 22.8 degrees
	- Range
		- Sonar head range: 1 to 200 meters
	- Profile range
		- 특정 임계값(Threshold)을 초과한 첫 번째 탐지된 거리 값을 샘플 단위로 표현
		- Range가 5m 미만일 경우: 1 sample unit = 2mm
		- Range가 5m 이상일 경우: 1 sample unit = 10mm
	- Echo
		- $N$=513 (500 Data Bytes, 500 Points)
			- Header: ASCII "IGX"
			- Data Bytes: 8
			  ![Pasted image 20241210152000.png|500](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241210152000.png)

<br/>

- SONAR Switch Data Command to SONAR Head
  ![Pasted image 20241210152712.png](/img/user/3_Archive/1_Attachments/Pasted%20image%2020241210152712.png)
	- Start gain
		- 0 to 40dB in 1dB increments
	- Sector width
		- 0 to 120 (0 to 360 degrees) in 3 degree steps
			- Sector width in degrees = Byte12 * 3
	- Train angle
		- 0 to 120 (-180 to +180 degrees) in 3 degree steps
			- Train angle in degrees = Byte11 * 3 - 180

- ROS Topic `ros_881a/data`
	- Range, StartGain, SectorWidth, TrainAngle, HeadPosition, ProfileRange, Echo(500 points)

<br/><br/>

## Message Type
### visualization_msgs/Marker

- Reference: https://wiki.ros.org/rviz/DisplayTypes/Marker
- Marker message에서 객체 타입을 `POINTS`로 하고, `geometry_msgs/Pose pose`에 임계값을 넘은 데이터들의 좌표 입력
- 단점: Intensity를 반영할 수 없음

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

<br/>

### sensor_msgs/PointCloud2
- `pcl::PointCloud<pcl::PointXYZI>`로 intensity까지 데이터에 포함할 수 있는 객체를 생성하고 `pcl::toROSMsg`를 통해 ROS 메시지로 변환
- 포인트 형태로 시각화 한다면 굳이 `visualization_msgs/Marker`를 사용할 필요가 없음

<br/><br/>

## 3D Visualization
- 881A 데이터를 `sensor_msgs/PointCloud2` 타입으로 변환하였으며, beam width를 고려하여, 10 degree 만틈 부채꼴로 포인트가 생성되게 하였음
	- Range는 10m이며, 500개의 포인트가 있기 때문에 각 포인트 별 거리는 0.02m ($r$)
	- Beam width 10 degree를 고려하여 0.1 degree 씩 포인트를 추가로 생성하여 부채꼴 형태의 포인트 생성 ($\theta$)
	- 극 좌표계 ($r, \theta, \phi$)를 센서 기준 직교 좌표계 ($x, y, z$)로 변환
	- Intensity가 threshold 이하인 포인트 필터링

![[Screencast from 2024년 12월 11일 02시 43분 42초.webm]]

```python fold
def polar_to_cartesian(r, theta, phi):
    """
    Convert polar coordinates (r, theta, phi) to Cartesian coordinates (x, y, z).
    
    Parameters:
        r (float): Radius (distance from origin to point)
        theta (float): Angle from z-axis (fixed at 90 degrees in this case)
        phi (float): Angle in the xz-plane from the x-axis
    
    Returns:
        tuple: Cartesian coordinates (x, y, z)
    """
    # Compute Cartesian coordinates
    x = r * math.cos(phi) * math.cos(theta)
    y = r * math.cos(phi) * math.sin(theta)
    z = r * math.sin(phi)

    return x, y, z

def create_points(echo, frequency, head_position, scan_range, threshold):
    num_points = len(echo)
    points_list = []  # 리스트로 변경
    step_dist = scan_range / num_points

    if frequency == 310:
        beam_width = 40
    elif frequency == 675:
        beam_width = 20
    elif frequency == 1000:
        beam_width = 10

    for i in range(num_points):
        r = i * step_dist

        for step in np.arange(0, beam_width, 0.1):  # 0.1씩 증가하는 루프
            theta = - beam_width / 2 + step
            theta = math.radians(theta)
            phi = math.radians(head_position)
            intensity = echo[i]
            
            if intensity >= threshold:
                x, y, z = polar_to_cartesian(r, theta, phi)
                points_list.append([x, y, z, intensity])  # 리스트에 추가

    points = np.array(points_list, dtype=np.float32)  # 최종적으로 배열로 변환
    return points

def create_pointcloud2(points, frame_id="map"):
    header = rospy.Header()
    header.stamp = rospy.Time.now()
    header.frame_id = frame_id
    
    fields = [
        PointField("x", 0, PointField.FLOAT32, 1),
        PointField("y", 4, PointField.FLOAT32, 1),
        PointField("z", 8, PointField.FLOAT32, 1),
        PointField("intensity", 12, PointField.FLOAT32, 1),
    ]
    
    point_cloud_data = [(p[0], p[1], p[2], p[3]) for p in points]
    
    return point_cloud2.create_cloud(header, fields, point_cloud_data)
```

<br/><br/>

### Transform to global coordinate
- 센서 기준 좌표계에서 월드 좌표계로 포인트들 변환
	- LiDAR에서 수상선의 위치인식 후 월드 좌표계에서의 x, y, z, roll, pitch, yaw를 구한 뒤 `/ros_881A/pose` topic으로 데이터를 주면 해당 위치로 센서 기준 좌표계를 이동

![[Screencast from 2024년 12월 11일 03시 00분 57초.webm]]

```python fold

def transform_matrix(x=0, y=0, z=0, roll=0, pitch=0, yaw=0):
    roll = math.radians(roll)
    pitch = math.radians(pitch)
    yaw = math.radians(yaw)
    
    R_roll = np.array([
        [1, 0, 0],
        [0, math.cos(roll), -math.sin(roll)],
        [0, math.sin(roll), math.cos(roll)]
    ], dtype = np.float32)
    
    R_pitch = np.array([
        [math.cos(pitch), 0, math.sin(pitch)],
        [0, 1, 0],
        [-math.sin(pitch), 0, math.cos(pitch)]
    ], dtype = np.float32)
    
    R_yaw = np.array([
        [math.cos(yaw), -math.sin(yaw), 0],
        [math.sin(yaw), math.cos(yaw), 0],
        [0, 0, 1]
    ], dtype = np.float32)
    
    R = R_yaw @ R_pitch @ R_roll
    T = np.array([x, y, z], dtype = np.float32)
    M = np.eye(4, dtype = np.float32)
    M[:3, :3] = R
    M[:3, 3] = T
    return M

def transform_point(points, x=0, y=0, z=0, roll=0, pitch=0, yaw=0):
    """
    Transform the input point cloud using the given translation and rotation.
    
    Args:
        points (np.ndarray): (N, 4) array with x, y, z, intensity.
        x, y, z (float): Translation values.
        roll, pitch, yaw (float): Rotation angles in degrees.
    
    Returns:
        np.ndarray: Transformed (N, 4) array with x, y, z, intensity.
    """
    # Extract x, y, z and create homogeneous coordinates
    xyz = points[:, :3]  # Extract (x, y, z)
    intensity = points[:, 3:]  # Extract intensity as a separate array
    points_xyz = np.hstack((xyz, np.ones((xyz.shape[0], 1))))  # Add homogeneous coordinate (N, 4)
    
    # Compute transformation matrix
    M = transform_matrix(x, y, z, roll, pitch, yaw)
    
    # Apply transformation
    transformed_points = np.dot(points_xyz, M.T)  # Resulting shape (N, 4)
    
    # Combine transformed coordinates with intensity
    transformed_xyz = transformed_points[:, :3]  # Extract transformed (x, y, z)
    return np.hstack((transformed_xyz, intensity))  # Combine with original intensity

# Define a global dictionary to store transform parameters
transform_params = {
    "x": 0.0,
    "y": 0.0,
    "z": 0.0,
    "roll": 0.0,
    "pitch": 0.0,
    "yaw": 0.0
}

def transform_params_callback(data):
    """
    Callback to update transform parameters dynamically.
    """
    try:
        global transform_params
        params = [float(x) for x in data.data.split(',')]
        transform_params["x"] = params[0]
        transform_params["y"] = params[1]
        transform_params["z"] = params[2]
        transform_params["roll"] = params[3]
        transform_params["pitch"] = params[4]
        transform_params["yaw"] = params[5]
        rospy.loginfo(f"Updated transform params: {transform_params}")
    except Exception as e:
        rospy.logerr(f"Error updating transform parameters: {e}")
```


## ROS Bag
- 수상선의 Jetson Orin에 ros_881a 패키지를 빌드하고, `{bash} rosrun ros_881a ros_881a` 로 881A 동작
- 결과 `ros_881a/data`, `ros_881a/ndata` 모두 정상적으로 publish 되었으며, ROS bagging 수행하였음
- NAS: `연구관련 프로그램 및 코드/PKRC/Data`

<br/><br/>

## 881A 수조 실험
- 881A raw data를 subscribe하여 sensor_msgs/PointCloud2 message 형식으로 publish
![3_Archive/1_Attachments/58a1718c632c4a3ef8fa3b5d799cc6dd_MD5.png|+grid](/img/user/3_Archive/1_Attachments/58a1718c632c4a3ef8fa3b5d799cc6dd_MD5.png)![3_Archive/1_Attachments/132f70363f8839547fdb8e2363d863bf_MD5.gif|+grid](/img/user/3_Archive/1_Attachments/132f70363f8839547fdb8e2363d863bf_MD5.gif)

<br/><br/>

## ros_881a_rviz_node.py
- 센서 좌표계 위치 조정
	- 현재는 x, y, z, roll, pitch, yaw가 주어지면 센서 좌표가 해당 위치로 이동하게 되어있음
	- LiDAR와 SONAR의 상대 위치를 고려하여 이동 필요
- Head position
	- 현재는 Head position을 Scan angle로 변환하여 시각화를 수행하는데 Train angle이 어떤 영향을 미치는지 파악
	- Train angle은 881A의 스캔 시작 위치를 뜻하며, 881A의 케이블 커넥터를 기준으로 정반대 방향이 0도로 되어있음

<br/><br/>

## 881A & MID360 코드 통합
![3_Archive/1_Attachments/feb9c7f807b66d09f413d935cb7d96df_MD5.gif](/img/user/3_Archive/1_Attachments/feb9c7f807b66d09f413d935cb7d96df_MD5.gif)
![3_Archive/1_Attachments/483ba7546d4d533217ad57fc287a16ce_MD5.jpg|+grid](/img/user/3_Archive/1_Attachments/483ba7546d4d533217ad57fc287a16ce_MD5.jpg)![3_Archive/1_Attachments/a6295da015e2fa3758b4572c0c09e42d_MD5.jpg|+grid](/img/user/3_Archive/1_Attachments/a6295da015e2fa3758b4572c0c09e42d_MD5.jpg)

<br/>

![3_Archive/1_Attachments/3bce89e795d0c618fa7dc35549d90f56_MD5.gif](/img/user/3_Archive/1_Attachments/3bce89e795d0c618fa7dc35549d90f56_MD5.gif)

![3_Archive/1_Attachments/d4badf2b290d7b35c09c75c543c5639a_MD5.jpg|+grid](/img/user/3_Archive/1_Attachments/d4badf2b290d7b35c09c75c543c5639a_MD5.jpg)![3_Archive/1_Attachments/ae875e86d974b6d6582f1e3108701e38_MD5.jpg|+grid](/img/user/3_Archive/1_Attachments/ae875e86d974b6d6582f1e3108701e38_MD5.jpg)

<br/><br/>

## ROS launch
- ros_881a.cpp 및 ros_881a_rviz_node.py 를 한번에 동작시키는 launch file 생성
	- Parameter를 수정시킬 수 있는 노드도 같이 동작시키도록 함

<br/><br/>

## ros_881a.cpp 수정 사항
- initCmd()
	- 현재는 initCmd() 내부에 변수들이 초기화 되어 있으며, main 문의 while에서 매 iteration 마다 initCmd() 호출
	- 해당 변수들을 한 번만 초기화한 뒤 ros topic 혹은 service를 사용하여 변수들을 조절할 수 있게 수정해야 함
- 코드 정리
	- 불필요한 주석 제거
	- Header 및 각 함수에 대한 설명 주석 추가

<br/><br/>

# Resource

