# jsk_pcl_ros

## Depth Camera Calibration(Kinect,Xtion,Primesense)

### Two Mail Steps:

*  `1. RGB Camera Calibration: Intrisic Calibration` `Please refer to ros RGB camera calibration tutorial` >> `http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration`

*  `2. Depth Calibration: Depth Calibration` related to the distance z, optical frame pixel u v and global pixel offset.

### U need:
   
*   Chessboard: Make sure ur Application Range, if u wanna use camera in short range(0.5~2m), choose small chessboard, or choose larger one. 
*   Depth Camera: Kinect one, Xtion, Primesense. (There may be some problem when using primesense, check `http://answers.ros.org/question/197318/openni2_launch-doesnt-work-with-carmine-109-connected-to-usb30/?comment=198397#comment-198397` and install the newest openni2, perhaps u need to do `apt-get remove libopenni2-0` first)
*   Good PC with ubuntu and ros installed:  We only tested in Lenovo thinkpad series.
*   jsk\_pcl\_ros:   `https://github.com/jsk-ros-pkg/jsk_recognition/tree/master/jsk_pcl_ros`

###
