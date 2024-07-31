# Bridging-Between-ROS1-and-ROS2-And-Operating-Turtlesim
This tutorial demonstrates how to establish a bridge between ROS1 (Noetic) and ROS2 (Foxy) using the ros1_bridge package. By following the instructions provided, you will learn to set up both ROS versions, run turtlesim nodes, and configure a dynamic bridge to enable seamless topic communication between the two ROS distributions.
# step 1 : install ROS2 
## set locale
```
locale  # check for UTF-8
  
  sudo apt update && sudo apt install locales
  sudo locale-gen en_US en_US.UTF-8
  sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
  export LANG=en_US.UTF-8

  locale  # verify settings ```
```


![telegram-cloud-photo-size-4-5850653344975143253-x](https://github.com/user-attachments/assets/a87f46e4-a9b9-4111-ab35-ac3141030800)



## setup source list 


```
sudo apt install software-properties-common
  sudo add-apt-repository universe
``` 

## add ROS 2 GPG key with apt

```

sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```
## add to source list 

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

## Installation
```
sudo apt update
  sudo apt install ros-foxy-desktop
  sudo apt install ros-dev-tools
```

## Environment Setup
```
echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
 source ~/.bashrc
```
 ## Start ROS1 (Noetic)

 ```
source /opt/ros/noetic/setup.bash
rosecore
```

## Start turtlesim in ROS2 (Foxy)

```
source /opt/ros/foxy/setup.bash
ros2 run turtlesim turtlesim_node
```

## Start turtlesim in ROS1 (Noetic)

```
source /opt/ros/noetic/setup.bash
rosrun turtlesim turtle_teleop_key
```
## Verify the Bridge

```
source /opt/ros/noetic/setup.bash
rosnode list
rostopic echo /turtle1/cmd_vel


ros2 node list
ros2 topic list
ros2 topic echo /turtle1/cmd_vel
```
## using ros1_ bridge 

```
sudo apt install ros-foxy-ros1-bridge
```
## Source both ROS1 and ROS2 setup files

```
source /opt/ros/noetic/setup.bash
source /opt/ros/foxy/setup.bash
```

## run the dynamic bridge 
```
ros2 run ros1_bridge dynamic_bridge
```


![telegram-cloud-photo-size-4-5850302746794771195-y](https://github.com/user-attachments/assets/1dda429c-7b1a-4a64-81ab-222ac7cbdc63)

**![telegram-cloud-photo-size-4-5850302746794771194-x](https://github.com/user-attachments/assets/7d1910c0-4e2c-48da-8e15-2d33473a6b48)
**


now you can run turtlesim from ros1 by using the bridge .
