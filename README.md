# ros_jetson

for the next experiment, we need finish the next steps.

step 1: prepare the necessary packages by flashing the OS
----Download and install the [NVIDIA Jetpack](https://developer.nvidia.com/embedded/jetpack).
    You will need to be running Ubuntu 14.04 on your host computer.

    Once Jetpack is up and running perform the following actions:

* Select TK1 as target board
* Click the `Clear Actions` button (upper right corner).  This will de-select all of the options.
* Select the following options for install:
    - `Driver for OS`
    - `File System`
    - `Flash OS`
    - `CUDA Toolkit for L4T`
    - `cuDNN Package`
    - `OpenCV for Tegra`
    - also select the box `Automatically resolve dependency conflicts`
* On the Network Layout page:
    - Select `Device accesses Internet via router/switch`
* On the Network Interface Selection page:
    - select `eth0` (assuming your host computer only has 1 ethernet)


After you have started the installation, the JetPack installer will download files and
install them.  As the installer continues, it will reach a point where it will flash the
OS to the Jetson board.  At this point, the installer will ask you to put the board into
Force USB Recovery Mode:

* Connect the micro USB cable to the Jetson TK1 and the host computer
* Plug the AC power adapter into AC power and connect the power jack to the board
* Enter USB Recovery Mode using the following sequence:
    - Press and release Power button
    - Hold down the Force Recovery button, then press and release Reset (while holding down Force Recovery)
    - You can check if the board is in Recovery mode by connecting to the Jetson board via ssh and running `lsusb`.  There should be a device with vendor 'NVidia Corp'
    - Begin the flashing process on the host by pressing Enter.  This will take several minutes.




And you can find the jetson.ino which is the code upload to the arduino!