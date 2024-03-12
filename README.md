# ROS Installation on Raspberry PI

## Requirements
1. Debian (Buster) OS on RPi
2. 16 GB+ Memory card
3. 2 GB+ RAM

## Installation

### Debian OS
    https://downloads.raspberrypi.org/raspios_full_armhf/images/raspios_full_armhf-2021-05-28/

### ROS Noetic setup
1. Update and Upgrade 
    ```
    sudo apt update
    sudo apt upgrade
    ```
        
2. Increase swap file if low RAM RPi is used 
    ```
    sudo dphys-swapfile swapoff
    sudo nano/etc/dphys-swapfile
    ```
    Inside the file change the 'CONF_SWAPSIZE' to desired value. (around 2GB).
    ```
    sudo dphys-swapfile setup
    sudo dphys-swapfile swapon
    ```

3. Follow below commands for installation
   ```
   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
   ```
   check for correct debian configuration
   ```
   cat /etc/apt/sources.list.d/ros-latest.list
   ```
   output should be as folows ```deb http://packages.ros.org/ros/ubuntu buster main``` <br>
   Set keys
   ```
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
   ```
   Update
   ```
   sudo apt update
   ```
   Install rosdep
   ```
   sudo apt-get install -y python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential cmake
   ```
   Initialize and update
   ```
   sudo rosdep init
   rosdep update
   ```
   Create a workspace for ROS
   ```
   mkdir catkin_ws
   cd catkin_ws
   ```
   Install ROS
   ```
   rosinstall_generator desktop --rosdistro noetic --deps --wet-only --tar > noetic-desktop-wet.rosinstall
   ```
   ```
   wstool init src noetic-desktop-wet.rosinstall
   ```
   ```
   rosdep install -y --from-paths src --ignore-src --rosdistro noetic -r --os=debian:buster
   ```
   Install and Build all packages (This may take hours based on RPi configuration)
   ```
   sudo src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILDTYPE=Release --install-space /opt/ros/noetic -j2 -DPYTHON_EXECUTABLE=/usr/bin/python3
   ```
4. Source the ROS files
   ```
   echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
   source ~/.bashrc
   ```
5. Check ros installation
   ```
   roscore
   ```
   








