## <center>TurtleBot-Tutorial
### <center>**Tutorial1**_ 模拟测试`TurtleBot Stage Simulator`_
>`Stage Simulator`是一个2-D多机器人模拟器,它模拟了.world文件中定义的世界。点击二维导航目标和命令机器人以导航地图中的任何位置。

```
roslaunch turtlebot_stage turtlebot_in_stage.launch
```
### <center>**Tutorial2** _制作地图并使用地图进行导航_
>说明：使用导航堆栈创建Gazebo世界的地图并基于它开始导航

#### 1.制作一张地图
首先调出Gazebo Bringup Guide中描述的TurtleBot模拟：
```
roslaunch turtlebot_gazebo turtlebot_world.launch
```
或者，您可以使用另一个现有的.world文件：
```
roslaunch turtlebot_gazebo turtlebot_world.launch world_file:=worlds/willowgarage.world
```
您可以通过设置TURTLEBOT_XXX环境变​​量来自定义模拟的TurtleBot; 例如：
```
$ export TURTLEBOT_BASE=create
$ export TURTLEBOT_STACKS=circles
$ export TURTLEBOT_3D_SENSOR=asus_xtion_pro
$ roslaunch turtlebot_gazebo turtlebot_playground.launch
```
#### 2.开始建立地图：
```
roslaunch turtlebot_gazebo gmapping_demo.launch
```
#### 3.使用RViz可视化地图构建过程：
```
roslaunch turtlebot_rviz_launchers view_navigation.launch
```
#### 4.通过键盘控制turtlebot来扫描
```
roslaunch turtlebot_teleop keyboard_teleop.launch
```
#### 5.将地图保存到磁盘：
```
rosrun map_server map_saver -f <your map name>
```
#### 6.导航
为确保所有内容都能按预期运行，请退出在前一节中启动的所有内容，并重复除地图构建外的所有步骤：
```
roslaunch turtlebot_gazebo amcl_demo.launch map_file:=<full path to your map YAML file>
```
或者，如果您更喜欢使用已经创建的地图，只需省略map_file参数即可。
### <center>**Tutorial3** _在gazebo上显示turtlebot_
#### 1.在TurtleBot上调出gazebo模型
```
roslaunch turtlebot_gazebo turtlebot_world.launch
```
#### 2.运行键盘控制
```
roslaunch turtlebot_teleop keyboard_teleop.launch
```
对于TurtleBot 2,可以使用kobuki_keyop工具：
```
roslaunch kobuki_keyop keyop.launch
```
#### 3.启动rviz仿真环境
````
roslaunch turtlebot_rviz_launchers view_robot.launch
````
### <center>**Tutorial4** _3D可视化_
#### 1.启动3D传感器
```
roslaunch turtlebot_bringup 3dsensor.launch
````
>如果您的机器人使用Kinect，请在启动3d传感器之前按照Kinect设置。
默认情况下，这将启动所有处理模块打开的3d传感器。您可以通过向启动命令发送适当的参数来关闭这些参数（有关更多信息，请参阅3dsensor.launch内部）。

#### 2.启动rviz已配置为可视化机器人及其传感器的输出：
```
roslaunch turtlebot_rviz_launchers view_robot.launch
```
#### 3.启用所需的显示
>DepthCloud
>
>Registered DepthCloud
>
>Image
>
>PointCloud
>
>Registered PointCloud

### <center>**Tutorial5**  _TurtleBot3 Simulation using Fake Node_
#### 1.首先在.bashrc添加下面代码
```
export TURTLEBOT3_MODEL=${TB3_MODEL}
export TURTLEBOT3_MODEL=waffle_pi
export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:~/turtlebot/src/turtlebot3/turtlebot3_gazebo_plugin/build
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/turtlebot/src/turtlebot3/turtlebot3_gazebo_plugin/models
```
在终端输入
```
source .bashrc
```
使环境生效

#### 2.在rviz上仿真
调出TurtleBot3机器人模型
```
roslaunch turtlebot3_fake turtlebot3_fake.launch
```
使TurtleBot3可以通过键盘控制
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
#### 3.使用gazebo模拟TurtleBot3
(1)调出TurtleBot3机器人模型
```
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```
(2)urtleBot3世界
>TurtleBot3 world是由构成TurtleBot3符号形状的简单对象组成的地图。TurtleBot3世界主要用于SLAM和导航等测试。

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
(3)TurtleBot3房子
>TurtleBot3 House是用房屋图纸制作的地图。它适用于涉及更复杂任务性能的测试。

```
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```
#### 4.在gazebo上驱动TurtleBot3
(1)遥控操作
>为了使用键盘控制TurtleBot3，请在新的终端窗口中使用以下命令启动遥控操作功能

```
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```
打开新终端
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
(2)避免碰撞
>为了自主驱动TurtleBot3世界的TurtleBot3，打开一个新的终端窗口并输入以下命令。

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
打开一个新的终端窗口并输入下面的命令
```
roslaunch turtlebot3_gazebo turtlebot3_simulation.launch
```
当模拟运行时，RViz可视化发布的主题。您可以通过输入以下命令在新的终端窗口中启动RViz
```
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```
#### 5.带有TurtleBot3的虚拟SLAM
>对于Gazebo中的虚拟SLAM，您可以选择上面提到的各种环境和机器人模型，而不是运行实际的机器人，而SLAM相关命令将使用SLAM部分中使用的ROS软件包。以下命令是使用TurtleBot3 Waffle Pi模型和turtlebot3_world环境的示例。

##### (1)启动gazebo
```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
##### (2)启动SLAM
```
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
##### (3)远程控制TurtleBot3
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
##### (4)保存地图
```
rosrun map_server map_saver -f ~/map
```
####6.虚拟导航与TurtleBot3
>对于Gazebo中的虚拟导航，您可以选择上面提到的各种环境和机器人模型，而不是运行实际的机器人，导航相关命令将使用导航部分中使用的ROS软件包。

##### (1)运行gazebo
```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
##### (2)导航
```
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
#### 7.由多TurtleBot3s虚拟SLAM
##### (1)在TurtleBot3 House中打三个TurtleBot3s
```
roslaunch turtlebot3_gazebo multi_turtlebot3.launch
```
##### (2)执行SLAM
```
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_0
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_1
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_2
```
##### (3)合并来自每个TurtleBot3的地图数据的地图数据
```
roslaunch turtlebot3_gazebo multi_map_merge.launch
```
##### (4)执行RViz
```
rosrun rviz rviz -d `rospack find turtlebot3_gazebo`/rviz/multi_turtlebot3_slam.rviz
```
##### (5)遥控操作
```
rosrun turtlebot3_teleop turtlebot3_teleop_key cmd_vel:=tb3_0/cmd_vel
```
##### (6)保存地图
```
rosrun map_server map_saver -f ~/map
```
### <center>**Tutorial6**  _TurtleBotOpenManipulator_
##### 1.安装相关依赖:
```
$ sudo apt-get install ros-kinetic-ros-controllers ros-kinetic-gazebo* ros-kinetic-moveit* ros-kinetic-dynamixel-sdk ros-kinetic-dynamixel-workbench-toolbox ros-kinetic-ar-track-alvar ros-kinetic-ar-track-alvar-msgs ros-kinetic-industrial-core
```
##### 2.首先在.bashrc添加下面代码
```
export TURTLEBOT3_MODEL=burger
export TURTLEBOT3_MODEL=waffle
export TURTLEBOT3_MODEL=waffle_pi
```
在终端输入
```
source .bashrc
```
使环境生效

##### 3.导出TurtleBot3_OpenManipulator模型
```
roslaunch open_manipulator_with_tb3_description open_manipulator_with_tb3_rviz.launch
```
##### 4.OpenCR安装程序
教程参考:[OpenCR Setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/manipulation/#hardware-setup)

##### 5.用OpenManipulator引导TurtleBot3
```
roslaunch open_manipulator_with_tb3_description open_manipulator_with_tb3_model.launch use_gazebo:=false
```
##### 6.SLAM
```
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_slam.launch use_gazebo:=false open_rviz:=true
```
##### 7.导航
```
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_navigation.launch use_gazebo:=false open_rviz:=true
```
##### 8.找到AR标记
```
roslaunch open_manipulator_ar_markers ar_pose.launch
```
##### 9.MoveIt！
```
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_manipulation.launch use_gazebo:=false open_rviz:=true
```
为了控制OpenManipulator的抓取器，请使用下面的命令在新的终端窗口中使用主题发布
```
rostopic pub /open_manipulator_with_tb3/gripper std_msgs/String "data: 'grip_off'" --once
```
##### 10.挑选和放置
>这里提供移动操作的拾取和放置示例。此示例由控制器启动，即自动启动和停止导航堆栈MoveIt！，通过传送ROS消息来选择和放置启动文件。用户可以修改此节点以应用其环境。

```
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_controller.launch
```
##### 11.模拟
>在Gazebo模拟器上用OpenManipulator加载TurtleBot3并单击Play按钮

```
roslaunch open_manipulator_with_tb3_gazebo open_manipulator_with_tb3_gazebo.launch
```
键入rostopic list以检查哪个主题已激活。
```
rostopic pub /joint4_position/command std_msgs/Float64 "data: 0.21" --once
```

>参考网站:
>
>http://learn.turtlebot.com/
>
>http://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#simulation
>
>https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/simulation.md
