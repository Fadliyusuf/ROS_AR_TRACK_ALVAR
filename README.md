# ROS_AR_TRACK_ALVAR

# Setup
Install the dependencies (this was tested on Ubuntu 18.04 with melodic):
```
$ sudo apt-get install ros-melodic-ar-track-alvar
$ sudo apt-get install ros-melodic-image-proc
$ sudo apt-get install ros-melodic-camera-calibration
$ sudo apt-get install libv4l-dev
$ sudo apt install ros-melodic-camera-info-manager*
```

using catkin workspaces which could be read about here:
```
http://wiki.ros.org/catkin/Tutorials/create_a_workspace
```
In catkin_ws/src I ran:
```
$ git clone https://github.com/Fadliyusuf/ROS_AR_TRACK_ALVAR.git
```
Back in /catkin_ws I ran:
```
$ catkin_make
```
# Calibration of USB camera
At this point you need to calibrate your camera. this tutorial will help on how to calibrate a monocular camera:
```
https://www.youtube.com/watch?v=UGArg1kQwFc
```
It would be a slightly different procedure if you were using a stereo camera.
NOTE: if using laptop usually (video0) is used for built-in cameras and (video2) is used for external cameras.
To change the camera you want to use, you can do it on: /catkin_ws/src/ROS_AR_TRACK_ALVAR/usb_cam/config/usb_cam.yaml
```
$ roslaunch usb_cam usb_cam-test.launch
```
```
$ rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.025 image:=/usb_cam/image_raw camera:=/usb_cam
```
move calibration data to:
/catkin_ws/src/RBE_ROS/sparki_bringup/data/calibration_data/ost.yaml

# Running
To run Ar Track Alvar on Rviz use:
```
$ roslaunch sparki_bringup rviz_field.launch
$ roslaunch sparki_bringup field_camera.launch
$ roslaunch sparki_bringup field_ar_markers.launch
```
 A static TF tree of the robots and field can be brought up with:
```
$ roslaunch sparki_bringup test_sparki_tf.launch
```


To display the travel line passed by the marker, you can use:
```
rosrun hector_trajectory_server hector_trajectory_server
```
NOTE: rename TF marker ar track alvar on file /catkin_ws/src/hector_slam/hector_trajectory_server/src/hector_trajectory_server.cpp
according to the marker used

# Make Marker
Create your first marker. Here I created a marker with the id ‘123’
```
$ rosrun ar_track_alvar createMarker 123
```
# NOTE
If an error occurs in the new terminal when running the command, use:
```
$ source devel/setup.bash
```

source1: https://github.com/ChrisBove/RBE_510_ROS/tree/master
source2: https://marielleeusebio.me/personal/2021/02/16/AR_tags.html
