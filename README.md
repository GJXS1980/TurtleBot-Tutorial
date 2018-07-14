## <center>TurtleBot-Tutorial
************************************
##### Installation dependence
```bash
sudo apt-get install ros-kinetic-ros-controllers ros-kinetic-gazebo* ros-kinetic-moveit* ros-kinetic-dynamixel-sdk ros-kinetic-dynamixel-workbench-toolbox ros-kinetic-ar-track-alvar ros-kinetic-ar-track-alvar-msgs ros-kinetic-industrial-core libsdl1.2-dev libsdl-image1.2-dev
```
##### Workstation_Setup
```bash
mkdir -p ~/turtlebot_ws/src
cd ~/turtlebot_ws/src
git clone https://github.com/GJXS1980/TurtleBot-Tutorial.git
git clone https://github.com/GJXS1980/slam_gmapping.git
git clone https://github.com/GJXS1980/navigation.git
cd ~/turtlebot_ws
catkin_make
echo "source ~/turtlebot_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

************************************
### <center>**Tutorial 1**  _TurtleBot3 Simulation using Fake Node_
#### 1.首先在.bashrc添加下面代码
```bash
export TURTLEBOT3_MODEL=${TB3_MODEL}
export TURTLEBOT3_MODEL=waffle_pi
export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:~/turtlebot/src/turtlebot3/turtlebot3_gazebo_plugin/build
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/turtlebot/src/turtlebot3/turtlebot3_gazebo_plugin/models
```
在终端输入
```bash
source .bashrc
```
使环境生效

#### 2.在rviz上仿真
调出TurtleBot3机器人模型
```bash
roslaunch turtlebot3_fake turtlebot3_fake.launch
```
使TurtleBot3可以通过键盘控制
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
#### 3.使用gazebo模拟TurtleBot3
(1)调出TurtleBot3机器人模型
```bash
roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```
(2)urtleBot3世界
>TurtleBot3 world是由构成TurtleBot3符号形状的简单对象组成的地图。TurtleBot3世界主要用于SLAM和导航等测试。

```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
(3)TurtleBot3房子
>TurtleBot3 House是用房屋图纸制作的地图。它适用于涉及更复杂任务性能的测试。

```bash
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```
#### 4.在gazebo上驱动TurtleBot3
(1)遥控操作
>为了使用键盘控制TurtleBot3，请在新的终端窗口中使用以下命令启动遥控操作功能

```bash
roslaunch turtlebot3_gazebo turtlebot3_house.launch
```
打开新终端
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
(2)避免碰撞
>为了自主驱动TurtleBot3世界的TurtleBot3，打开一个新的终端窗口并输入以下命令。

```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
打开一个新的终端窗口并输入下面的命令
```bash
roslaunch turtlebot3_gazebo turtlebot3_simulation.launch
```
当模拟运行时，RViz可视化发布的主题。您可以通过输入以下命令在新的终端窗口中启动RViz
```bash
roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch
```
#### 5.带有TurtleBot3的虚拟SLAM
>对于Gazebo中的虚拟SLAM，您可以选择上面提到的各种环境和机器人模型，而不是运行实际的机器人，而SLAM相关命令将使用SLAM部分中使用的ROS软件包。以下命令是使用TurtleBot3 Waffle Pi模型和turtlebot3_world环境的示例。

##### (1)启动gazebo
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
##### (2)启动SLAM
```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
##### (3)远程控制TurtleBot3
```bash
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
##### (4)保存地图
```bash
rosrun map_server map_saver -f ~/map
```
####6.虚拟导航与TurtleBot3
>对于Gazebo中的虚拟导航，您可以选择上面提到的各种环境和机器人模型，而不是运行实际的机器人，导航相关命令将使用导航部分中使用的ROS软件包。

##### (1)运行gazebo
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
##### (2)导航
```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
#### 7.由多TurtleBot3s虚拟SLAM
##### (1)在TurtleBot3 House中打三个TurtleBot3s
```bash
roslaunch turtlebot3_gazebo multi_turtlebot3.launch
```
##### (2)执行SLAM
```bash
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_0
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_1
roslaunch turtlebot3_gazebo multi_turtlebot3_slam.launch ns:=tb3_2
```
##### (3)合并来自每个TurtleBot3的地图数据的地图数据
```bash
roslaunch turtlebot3_gazebo multi_map_merge.launch
```
##### (4)执行RViz
```bash
rosrun rviz rviz -d `rospack find turtlebot3_gazebo`/rviz/multi_turtlebot3_slam.rviz
```
##### (5)遥控操作
```bash
rosrun turtlebot3_teleop turtlebot3_teleop_key cmd_vel:=tb3_0/cmd_vel
```
##### (6)保存地图
```bash
rosrun map_server map_saver -f ~/map
```

************************************
### <center>**Tutorial 2**  _TurtleBotOpenManipulator_
##### 1.首先在.bashrc添加下面代码
```bash
export TURTLEBOT3_MODEL=burger
export TURTLEBOT3_MODEL=waffle
export TURTLEBOT3_MODEL=waffle_pi
```
在终端输入
```bash
source .bashrc
```
使环境生效

##### 2.导出TurtleBot3_OpenManipulator模型
```bash
roslaunch open_manipulator_with_tb3_description open_manipulator_with_tb3_rviz.launch
```
##### 3.OpenCR安装程序
教程参考:[OpenCR Setup](http://emanual.robotis.com/docs/en/platform/turtlebot3/manipulation/#hardware-setup)

##### 4.用OpenManipulator引导TurtleBot3
```bash
roslaunch open_manipulator_with_tb3_description open_manipulator_with_tb3_model.launch use_gazebo:=false
```
##### 5.SLAM
```bash
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_slam.launch use_gazebo:=false open_rviz:=true
```
##### 6.导航
```bash
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_navigation.launch use_gazebo:=false open_rviz:=true
```
##### 7.找到AR标记
```
roslaunch open_manipulator_ar_markers ar_pose.launch
```
##### 8.MoveIt！
```bash
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_manipulation.launch use_gazebo:=false open_rviz:=true
```
为了控制OpenManipulator的抓取器，请使用下面的命令在新的终端窗口中使用主题发布
```bash
rostopic pub /open_manipulator_with_tb3/gripper std_msgs/String "data: 'grip_off'" --once
```
##### 9.挑选和放置
>这里提供移动操作的拾取和放置示例。此示例由控制器启动，即自动启动和停止导航堆栈MoveIt！，通过传送ROS消息来选择和放置启动文件。用户可以修改此节点以应用其环境。

```bash
roslaunch open_manipulator_with_tb3_tools open_manipulator_with_tb3_controller.launch
```
##### 10.模拟
>在Gazebo模拟器上用OpenManipulator加载TurtleBot3并单击Play按钮

```bash
roslaunch open_manipulator_with_tb3_gazebo open_manipulator_with_tb3_gazebo.launch
```
键入rostopic list以检查哪个主题已激活。
```bash
rostopic pub /joint4_position/command std_msgs/Float64 "data: 0.21" --once
```

************************************
>参考网站:
>
>http://learn.turtlebot.com/
>
>http://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#simulation
>
>https://github.com/ROBOTIS-GIT/emanual/blob/master/docs/en/platform/turtlebot3/simulation.md

************************************