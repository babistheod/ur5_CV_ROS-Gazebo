### Implementation of UR5 pick and place in ROS-Gazebo with a USB cam and vacuum grippers. 

This project was tested in Ubuntu 16.04 with ROS kinetic.
- Make sure you have installed Python2.7 and some useful libraries/packages, such as Numpy, cv2, etc.
- Install ROS kinetic, Gazebo, universal robot, Moveit, RViz. 
- Assuming your universal robot workspace is named as `ur_ws`, download the repository to `ur_ws/src/`
- Under `ur_ws/src`, there are two folders: one is the official `universal_robot`, and the other is `ur5_ROS-Gazebo`. Open file `ur5_joint_limited_robot.urdf.xacro` under `ur_ws/src/universal_robot/ur_description/urdf/`, and __make the following change to the joint limit:__
  ```
    shoulder_pan_lower_limit="${-2*pi}" shoulder_pan_upper_limit="${2*pi}"
  ```
- In the same directory, make a copy of `common.gazebo.xacro` and `ur5.urdf.xacro` in case of any malfunction. 
These two default files do not include camera and vacuum gripper modules. 
So we would replace these two files with customized files. 
Under directory `ur_ws/src/ur5_ROS-Gazebo/src/ur_description/`, copy `common.gazebo.xacro` and `ur5.urdf.xacro` to `ur_ws/src/universal_robot/ur_description/urdf/`.
- Build the code under directory `ur_ws/`,
  ```
  $ catkin_make
  $ source devel/setup.bash  
  ```
- Run the code with ROS and Gazebo
  ```
  $ roslaunch ur5_notebook init.launch 
  ```
- Things to work on: (1) vacuum grippers only provide limited force for lifting, so we had to use so many of them in order to pick up a light box. If you have any suggestions, please let us know. (2) UR5 motion planning is not in realtime, and hence you can ovserve a non-smooth motion of the end-effect in the camera view. 
 

#### 0. References
-Huang, L., Zhao, H., Implementation of UR5 pick and place in ROS-Gazebo with a USB cam and vacuum grippers, (2018), GitHub repository,         (https://github.com/lihuang3/ur5_ROS-Gazebo.git)
- [__`GitHub: utecrobotics/ur5`__](https://github.com/utecrobotics/ur5) testing ur5 motion
- [__`Very useful ROS blog`__](http://www.guyuehome.com/column/ros-explore) ROS探索
- [__`ROS下如何使用moveit驱动UR5机械臂`__](http://blog.csdn.net/jayandchuxu/article/details/54693870)
- [__`ROS UR industrial`__](http://wiki.ros.org/universal_robot/Tutorials/Getting%20Started%20with%20a%20Universal%20Robot%20and%20ROS-Industrial)
- [__`ROS modern driver`__](https://github.com/iron-ox/ur_modern_driver)
- [__`ur_hardware_interface.cpp`__](https://github.com/iron-ox/ur_modern_driver/blob/883070d0b6c0c32b78bb1ca7155b8f3a1ead416c/src/ur_hardware_interface.cpp) Replace this cpp
