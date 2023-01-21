# Setting up turtlebot3 with Jetson Nano 2GB
## Installing Jetpack
- Download Jetson Pack <a href="https://developer.nvidia.com/jetson-nano-2gb-jp45-sd-card-image" target="_blank">[recommending Jetpack 4.5]</a>, <a href="https://forums.developer.nvidia.com/t/not-able-to-boot-up-from-sd-card-using-jetson-nano-2gb-board/216764">because of booting error.</a>
- <a href="https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write">Write Jetson Pack on SD Card.</a>

## Checks
- Ensure connection to internet
- Ensure OpenCR is plugged to Jetson
- Levitate the whole robot if already assembled

## Installing SBC

```
sudo apt-get update -y
```
```
sudo apt-get install -y chrony ntpdate build-essential curl nano
```
```
sudo ntpdate ntp.ubuntu.com
```
### <a href="http://wiki.ros.org/melodic/Installation/Ubuntu">ROS</a> setup
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
```
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```
```
sudo apt-get update -y
```
```
sudo apt install ros-melodic-ros-base
```
```
sudo apt install python-rosdep -y
```
```
sudo rosdep init
```
```
rosdep update
```
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
```
```
sudo apt-get install ros-melodic-rosserial-python ros-melodic-tf ros-melodic-hls-lfcd-lds-driver ros-melodic-turtlebot3-msgs ros-melodic-dynamixel-sdk -y
```
```
git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
cd turtlebot3
rm -r turtlebot3_description/ turtlebot3_teleop/ turtlebot3_navigation/ turtlebot3_slam/ turtlebot3_example/
```
```
source /opt/ros/melodic/setup.sh
```
```
cd ~/catkin_ws/ && catkin_make
```
```
source ~/.bashrc
```

## Setting up <a href="https://emanual.robotis.com/docs/en/platform/turtlebot3/opencr_setup/#opencr-setup"> OpenCR</a>
```
sudo dpkg --add-architecture armhf
sudo apt-get update
```
```
sudo apt-get install libc6:armhf -y

export OPENCR_PORT=/dev/ttyACM0
export OPENCR_MODEL=waffle
```
```
wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/opencr_update.tar.bz2 
tar -xvf opencr_update.tar.bz2 
rm -rf ./opencr_update.tar.bz2
```
```
sudo chmod a+rw /dev/ttyACM0
```
```
cd ./opencr_update
sudo ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr
```
```
wget https://raw.githubusercontent.com/ROBOTIS-GIT/OpenCR/master/99-opencr-cdc.rules
```
```
sudo cp ./99-opencr-cdc.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger
```

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/fGEq_0aWpoA/0.jpg)](https://www.youtube.com/embed/fGEq_0aWpoA)
