# Please don’t update to ubuntu 16.04!!!!!
#### (if you have the usb-installer, all the files can be found from it, if not, please follow the requirement of software versions when you download)
# If you have, please do the following line first:
##### optimize the system firstly
<p> open the terminal and run the next command line from 3 to
6 when you find the file
1. find where is the 1_configureSystem.sh
2. go to that file by **cd**
3. to give the execute permission, run `sudo chmod 777*`
4. and `./1_configureSystem.sh`
5. ` ./2_install_grinch.sh`
6. reboot the computer to update by `sudo reboot`

### if not
### 1. Install CUDA 6.5
<p> run the command line in the terminal
- `sudo apt-get -y install libgomp1 libfreeimage-dev libopenmpi-dev openmpi-bin mesa-common-dev freeglut3-dev`
- `sudo dpkg -i cuda-repo-l4t-r21.5-6-5-local_6.5-53_armhf.deb` <p>**this line should be implemented in the folder which has this __.deb file**
<p> just use `cd /your file path`
<p> and then run the update command:
- `sudo apt-get update`
- `sudo apt-get -y install cuda-toolkit-6-5`
## set the local environment
<p> to open the environment setting files,run the
- `sudo echo 'export CUDAHOME=/usr/local/cuda' >> ~/.bashrc`
- `sudo echo 'export PATH=$CUDAHOME/bin:$PATH' >> ~/.bashrc`
- `sudo echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CUDAHOME/lib' >> ~/.bashrc`
<p> you can cheak whether these paths have been written in the bashrc, by run `gedit ~/.bashrc`
- `source ~/.bashrc`
- `sudo sh -c 'echo "/usr/local/cuda/lib" >> /etc/ld.so.conf.d/nvidia-tegra.conf`
- `1sudo ldconfig -v`
## check whether you are successful
<p> run the following command to check the output
- `nvcc -V`
- check whether the information will be shown on the screen :
  > <p> nvcc: NVIDIA (R) Cuda compiler driver
  > <p>Copyright (c) 2005-2014 NVIDIA Corporation
  > <p>Built on Tue_Feb_17_22:53:16_CST_2015
  > <p>Cuda compilation tools, release 6.5, V6.5.45

## 2. install cudnn and opencv
### (please first download the version 2 of cudnn and uncompress it)
## cudnn
- go to the file where you umcompress the cudnn, `cd /path`
<p> and run the command to create the softlink:
- `sudo cp *.h /usr/local/cuda/include`
- `sudo cp libcudnn* /usr/local/cuda/lib # cd /usr/local/cuda/lib`
-` sudo rm libcudnn.so libcudnn.so.6.0`
- `sudo ln -s libcudnn.so.6.5.48 libcudnn.so.6.5`
- `sudo ln -s libcudnn.so.6.5 libcudnn.so`
- `sudo ldconfig -v`

## Opencv:
### (please download the version 2.4.13 of opencv with the .deb file!!! )
- `sudo apt-get update`
<p> install the necessay Dependencies:
- `sudo apt-get install -y libopencv4tegra libopencv4tegra-dev libopencv4tegra-python`
## check!!!!
 > <p>python
  > <p> >>> import cv2
  > <p> >>> print cv2.__version__  
Check whether terminal will show the information of version

# 3.install ros (jade)
## 1 easy way by the shell.sh file
<p> if you can `git clone https://github.com/ywangeq/ros_jetson.git` successfully, you can find a **.sh** in the sources

-    sudo apt-get install git
-    mkdir -p ~/catkin_ws/src; cd ~/catkin_ws/src  
-    git clone https://github.com/ywangeq/ros_jetson.git
###### (i am not sure this rep is open to you)  
> make sure you download this file in `catkin_ws/src` by `cd ~/catkin_ws/src`
<p> and directly run the shell by `sudo ./rosjet_install.sh`



## 2 install manually
<p> run all the command in the terminal
#### Configure time-zone
- `sudo dpkg-reconfigure tzdata`


#### Ros Prerequisites
- `sudo update-locale LANG=C LANGUAGE=C LC_ALL=C LC_MESSAGES=POSIX`
- `sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'`
- `wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -`
- `sudo apt-get update`

#### Ros Jade Base bulid
- `sudo apt-get -y install ros-jade-ros-base`

#### install Python Dependencies
- `sudo apt-get -y install python-rosdep python-dev python-pip python-rosinstall python-wstool`

- `sudo rosdep init`
- `rosdep update`
- `echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc`
- `source ~/.bashrc`

### necessay Ros packages
- sudo apt-get -y install ros-jade-rosserial-arduino
- sudo apt-get -y install ros-jade-rosserial
- sudo apt-get -y install ros-jade-eigen-conversions
- sudo apt-get -y install ros-jade-tf2-geometry-msgs
- sudo apt-get -y install ros-jade-angles
- sudo apt-get -y install ros-jade-web-video-server
- sudo apt-get -y install ros-jade-rosbridge-suite
- sudo apt-get -y install ros-jade-rospy-tutorials
- sudo apt-get -y install ros-jade-joy
- sudo apt-get -y install ros-jade-teleop-twist-joy
- sudo apt-get -y install ros-jade-roslint
- sudo apt-get -y install ros-jade-controller-manager
- sudo apt-get -y install ros-jade-camera-calibration-parsers
- sudo apt-get -y install ros-jade-xacro
- sudo apt-get -y install ros-jade-robot-state-publisher
- sudo apt-get -y install ros-jade-diff-drive-controller
- sudo apt-get -y install ros-jade-usb-cam
- sudo apt-get -y install ros-jade-ros-control
- sudo apt-get -y install ros-jade-dynamic-reconfigure
- sudo apt-get -y install ros-jade-fake-localization
-sudo apt-get -y install ros-jade-joint-state-controller

### Configure Catkin Workspace
- run `source /opt/ros/jade/setup.bash` to upload the ros environment
- go to the src of Workspace by `cd ~/catkin_ws/src`
- and initialize the Workspace by `catkin_init_workspace`



### Install Ros Opencv bindings from source
- go back the Workspace `cd ~/catkin_ws`
> `cd src`
> <p> create a file called rosjet.rosinstall in the src
> the content is be shown next, you can just copy it.
<p>- tar:
    local-name: libraries/image_common/camera_info_manager
    uri: https://github.com/ros-gbp/image_common-release/archive/release/jade/camera_info_manager/1.11.10-0.tar.gz
    version: image_common-release-release-jade-camera_info_manager-1.11.10-0
<p>- tar:
    local-name: libraries/image_common/image_transport
    uri: https://github.com/ros-gbp/image_common-release/archive/release/jade/image_transport/1.11.10-0.tar.gz
    version: image_common-release-release-jade-image_transport-1.11.10-0
<p>- tar:
    local-name: libraries/usb_cam
    uri: https://github.com/bosch-ros-pkg-release/usb_cam-release/archive/release/jade/usb_cam/0.3.4-0.tar.gz
    version: usb_cam-release-release-jade-usb_cam-0.3.4-0
<p>- tar:
    local-name: libraries/vision_opencv/cv_bridge
    uri: https://github.com/ros-gbp/vision_opencv-release/archive/release/jade/cv_bridge/1.11.12-0.tar.gz
    version: vision_opencv-release-release-jade-cv_bridge-1.11.12-0
<p>

-and run the command `wstool init src`

- `wstool merge -t src src/rosjet.rosinstall`
- `wstool update -t src`

# 4.System Optimizations
you can directly run these commands in the terminal:
- gsettings set org.gnome.settings-daemon.plugins.power button-power shutdown
- gsettings set org.gnome.desktop.screensaver lock-enabled false
- sudo apt-get -y install compizconfig-settings-manager
- gsettings set org.gnome.desktop.interface enable-animations false
- gsettings set com.canonical.Unity.Lenses remote-content-search none
- echo -e '[SeatDefaults]\nautologin-user=ubuntu' > login_file; sudo mv login_file /etc/lightdm/lightdm.conf
- gsettings set org.gnome.Vino enabled true
- gsettings set org.gnome.Vino disable-background true
- gsettings set org.gnome.Vino prompt-enabled false
- gsettings set org.gnome.Vino require-encryption false
- echo "alias sr='source ~/catkin_ws/devel/setup.bash'" >> ~/.bashrc
- go to the src of Workspace `cd ~/catkin_ws`
- and build the source `catkin_make && source devel/setup.sh`
