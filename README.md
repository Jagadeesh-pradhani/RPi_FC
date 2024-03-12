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
