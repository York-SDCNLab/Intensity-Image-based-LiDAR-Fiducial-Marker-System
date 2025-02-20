# Intensity Image-based LiDAR Fiducial Marker System
![2489_graph](https://github.com/York-SDCNLab/IILFM/assets/58899542/6d58d12c-9939-474a-a99b-3bb1c2de8ae6)

This work has been accepted by the [IEEE Robotics and Automation Letters.](https://ieeexplore.ieee.org/document/9774900) <br>
<br>
YouTube link to the introduction video: https://www.youtube.com/watch?v=AYBQHAEWBLM. <br>
Bilibili link to the introduction video: https://www.bilibili.com/video/BV1s34y147UM/. <br>
<br>
:tada::tada::tada:News! <br>
:mega: The first mapping and localization framework based on LiDAR fiducial markers has been released [here](https://github.com/yorklyb/LiDAR-SFM)! Check out the instance reconstruction results below. The top row displays the ground truth on the left and [ours](https://github.com/yorklyb/LiDAR-SFM) on the right. The bottom row shows [Livox Mapping](https://github.com/Livox-SDK/livox_mapping) on the left and [LOAM Livox](https://github.com/hku-mars/loam_livox) on the right. <br>
<img width="250" height="150" src="https://github.com/yorklyb/LiDAR-SFM/assets/58899542/a1eba0cf-f41f-4d7a-89e3-4e31194c628a"/> <img width="250" height="150" src="https://github.com/yorklyb/LiDAR-SFM/assets/58899542/939e7ca6-b916-4831-a24d-869b6dc61686"/> <br>
<img width="250" height="150" src="https://github.com/yorklyb/LiDAR-SFM/assets/58899542/cdaa5904-da4d-46ed-9f7a-9b063fd5c1df"/> <img width="250" height="150" src="https://github.com/yorklyb/LiDAR-SFM/assets/58899542/264ba542-7c4e-4f93-b0d3-6430ed96a920"/> <br>

:mega: Our new work [	Fiducial Tag Localization on a 3D LiDAR Prior Map ](https://github.com/York-SDCNLab/Marker-Detection-General) has been released! <br>
## Background
Extensive research has been carried out on the Visual Fiducial Marker (VFM) systems. However, no single study utilizes these systems to their fullest potential in LiDAR applications. In this work, we develop an Intensity Image-based LiDAR Fiducial Marker (IILFM) system that fills the above-mentioned gap. The proposed system only requires an unstructured point cloud with intensity as the input and it outputs the detected markers' information and the 6-DOF pose that describes the transmission from the world coordinate system to the LiDAR coordinate system. The use of the IIFLM system is as convenient as the conventional VFM systems with no restrictions on marker placement and shape. Different VFM systems, such as [Apriltag 3](https://github.com/AprilRobotics/apriltag), [ArUco](https://docs.opencv.org/3.4/d5/dae/tutorial_aruco_detection.html), and [CCTag](https://cctag.readthedocs.io/en/latest/), can be easily embedded into the system. Hence, the proposed system inherits the functionality of the VFM systems, such as the coding and decoding methods.<br>
<img width="400" height="400" src="https://user-images.githubusercontent.com/58899542/151822834-e7758e70-849f-483d-b2fd-df93b1fe0aa5.png"/> <br>
## Marker Detection Demos
One and Two markers detection:
![demo1](https://user-images.githubusercontent.com/58899542/151841293-f2f4f2d0-f5ba-427e-b5e7-ff6106e4a8d0.gif)
Apriltag grid (35 markers) detection:<br>
<img width="480" height="320" src="https://user-images.githubusercontent.com/58899542/152581823-ca10f8db-8d3e-4025-91e9-eb111489b911.jpeg"/> <br>
![demo2](https://user-images.githubusercontent.com/58899542/152580373-71096105-8b6a-47ba-a852-767922dcf39a.gif)
![demo3](https://user-images.githubusercontent.com/58899542/152580126-5306eb2e-7899-494a-a7bd-bb0f43427daa.gif)
## LiDAR Pose Estimation Demo
![demo4](https://user-images.githubusercontent.com/58899542/152581365-ff25f9c3-3fd2-4a1d-9525-2383717266b3.gif)

## Other Applications
The proposed system shows potential in augmented reality, SLAM, multisensor calbartion, etc. Here, an augumented reality demo using the proposed system is presented. The teapot point cloud is transmitted to the location of the marker in the LiDAR point cloud based on the pose provided by the IILFM system. <br>
![demo5](https://user-images.githubusercontent.com/58899542/152583787-add4a9f2-59c6-4e15-a112-f1d2ad10324e.gif) <br>
In this repository, we only release the version of which the embedded system is [Apriltag 3](https://github.com/AprilRobotics/apriltag). The versions with [ArUco](https://docs.opencv.org/3.4/d5/dae/tutorial_aruco_detection.html), [CCTag](https://cctag.readthedocs.io/en/latest/) detectors are coming soon. It is a very straightforward process to replace the embedded visual fiducial marker system. Hence, following the method introduced in our scripts, you may add any visual marker detector as you like.



## Requirements
* Ubuntu 20.04 <br>
Other versions of the Ubuntu system could work if the following libraries are installed correctly.<br>
* ROS Noetic <br>
[Ubuntu install of ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu)<br>
Lower ROS versions could work. Yet you might have to deal with the conflicts of OpenCV4 and OpenCV3...
* PCL <br>
``sudo apt update``<br>
``sudo apt install libpcl-dev``<br>
* OpenCV <br>
``sudo apt update``<br>
``sudo apt install libopencv-dev python3-opencv``<br>
* catkin<br>
``sudo apt update``<br>
``sudo apt install catkin``<br>
* yaml-cpp <br>
``sudo apt update``<br>
``sudo apt-get install libyaml-cpp-dev``<br>
* Boost <br>
``sudo apt update``<br>
``sudo apt-get install libboost-all-dev``

## Commands
```git clone https://github.com/York-SDCNLab/IILFM.git```<br>
```cd IILFM```<br>
```catkin build```<br>
<br>
Modify the '**yorktag.launch**' in ~/IILFM/src/yorkapriltag/launch according to your LiDAR model (e.g. rostopic, angular resolutions, and so on) and the employed tag family. Then modify the '**config.yaml**' in ~/IILFM/src/yorkapriltag/resources based on your setup (define the locations of the vertices with respect to the world coordinate system). Otherwise, the outputted pose is meaningless. Afterward, run <br>
```source ./devel/setup.bash```<br>
```roslaunch yorkapriltag yorktag.launch```<br>
Open a new terminal in ~/IILFM/src/yorkapriltag/resources and run <br>
```rosbag play -l bagname.bag```<br>
<br>
To view the 6-DOF pose, open a new terminal and run<br>
``rostopic echo /iilfm/pose`` <br>
<br>
To view the point could of the detected 3D fiducials in rviz, open a new terminal and run rviz. In rviz, change the 'Fixed Frame' to 'livox_frame'. ``add/ By topic/ iilfm/ features/ PointCloud2``<br>
<br>
* By default, the settings in '**yorktag.launch**' are corresponding to Livox Mid-40. If you just want to try our system and see how it works, there is no need to modify '**yorktag.launch**' and '**config.yaml**'. You may simply run <br>
```source ./devel/setup.bash```<br>
```roslaunch yorkapriltag yorktag.launch```<br>
Then, in ~/IILFM/src/yorkapriltag/resources, open a new terminal and run <br>
```rosbag play -l bagname.bag```<br>

## Experimental result:
Due to the page limitation, we removed this huge table from our manuscript submitted to RA-L and replaced it with a histogram. Considering that some readers might be interested in the ground truth, we present the table here. Please refer to our paper to see the detailed experimental setup.
![table1](https://user-images.githubusercontent.com/58899542/162066700-d5afbac9-aa5e-49b9-a4d6-648e8bb8956c.png)

# Citation
If you find this work helpful for your research, please cite our [paper](https://ieeexplore.ieee.org/document/9774900):
```
@ARTICLE{9774900,
  author={Liu, Yibo and Schofield, Hunter and Shan, Jinjun},
  journal={IEEE Robotics and Automation Letters}, 
  title={Intensity Image-Based LiDAR Fiducial Marker System}, 
  year={2022},
  volume={7},
  number={3},
  pages={6542-6549},
  doi={10.1109/LRA.2022.3174971}}
```

