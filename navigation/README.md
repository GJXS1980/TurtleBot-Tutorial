## navigation
*******************************
##### Installation dependence
```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt-get update
sudo apt-get install ros-kinetic-bfl 
```

*******************************
##### Workstation_Setup
```bash
mkdir -p ~/navigation_ws/src
cd ~/navigation_ws/src
git clone https://github.com/GJXS1980/navigation.git
cd ~/navigation_ws
catkin_make
echo "source ~/navigation_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

****************************************
>Reference
>
>[moriarty/navigation](https://github.com/moriarty/navigation)
>
>[ros-planning/navigation](https://github.com/ros-planning/navigation)

****************************************











