# jsk_pcl_ros

## Depth Camera Calibration(Kinect,Xtion,Primesense)

### Two Mail Steps:

*  `1. Camera Intrisic Calibration: Intrisic Calibration` `Please refer to ros RGB camera calibration tutorial` >> `http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration`

*  `2. Depth Calibration: Depth Calibration` related to the distance z, optical frame pixel u v and global pixel offset.

### You need:
   
*   Chessboard: Make sure ur Application Range, if u wanna use camera in short range(0.5~2m) choose small chessboard, otherwise plz choose a larger one. 
*   Depth Camera: Kinect one, Xtion, Primesense. (There may be some problem when using primesense, check `http://answers.ros.org/question/197318/openni2_launch-doesnt-work-with-carmine-109-connected-to-usb30/?comment=198397#comment-198397` to install the newest openni2, perhaps u need to do `apt-get remove libopenni2-0` first)
*   Good PC with ubuntu and ros installed:  We only tested in Lenovo thinkpad series.
*   jsk\_pcl\_ros:   `https://github.com/jsk-ros-pkg/jsk_recognition/tree/master/jsk_pcl_ros`

### Camera Intrisic Calibration:

* Please follow `http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration` tutorial and when U finished calibration(4 features become green), wait patiently until u can click upload, calibration file will be right there in `~/.ros/camera_info/***.yaml` waiting.  `Check the openni2_launch.launch file or openni2_local.launch if u use JSK package to edit the path`

* For Details Please Refer to `Zhang, Zhengyou. "A flexible new technique for camera calibration." Pattern Analysis and Machine Intelligence, IEEE Transactions on 22.11 (2000): 1330-1334.`

###Depth Calibration(Available only in jsk\_pcl\_ros package):
We assume the intrisic calibration has been performed well.

* Plug in ur depth camera and run `roslaunch jsk\_pcl\_ros openni2\_local.launch` and `roslaunch jsk\_pcl\_ros openni2\_remote.launch` (Load the camera intrisic calibration file)

* Do `roscd jsk\_pcl\_ros` and `cd launch`, find file `depth\_error.launch` edit param `rect0_size_x` `rect0_size_y` and  `grid0_size_x` `grid0_size_y` according to your chessboard. Then `roslaunch jsk\_pcl\_ros depth\_error.launch`

* Open new CMD and run `rosrun image\_view image\_view image:=/depth_error_linear_regression/frequency_map`

* Do `rosrun rviz rviz` and subscribe to 3 topics(two pointcloud2 and one Pose)

Pose `/checkerdetector/objectdetection\_pose`

Raw Pointcloud `/camera\_remote\_uncalibrated/depth\_registered/points`

Calibrated Pointcloud ``/camera\_remote/depth\_registered/points``

You will see the Error between Pose(Estimated by rbg camera while looking at chessboard) and uncalibrated
camera

* Open another CMD and run `rosrun jsk\_pcl\_ros depth\_error\_calibration.py --model quadratic-uv-quadratic-abs`






