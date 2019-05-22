# Jetson-TX2_Documentation

## Initial Setup of Jetson TX2 
### Setup with a Ubuntu Host Computer
If you are using a host computer with ubuntu 16.04 or 18.04 installed, then simply follow the installation guide provided by nvidia [here](https://docs.nvidia.com/jetson/l4t/index.html#page/Tegra%2520Linux%2520Driver%2520Package%2520Development%2520Guide%2Fquick_start.html%23) . 
This will install the Nvidia Tegra onto the boards. You will need a ethernet cable, and micro usb data cord to flash Tegra onto the board.

### Setup without a Ubuntu Host Computer (Centos7)
To flash Jetson Developer Kit operating software:
1. Ensure that a Micro Usb, Ethernet, Power Adapter, and mouse are connected to the Board. The Micro USB and Ethernet are connected from the Host Computer to the Board.
2. The current L4T (Tegra Linux Driver Package) provides the necessary tools to flash your developer kit. The package used was the Nvidia L4T 32.1. Generally, use the most current L4T Package provided. Download the most current package and sample file system for your Kit from the [here](https://developer.nvidia.com/linux-tegra). 
3. Untar the files and assemble the rootfs:
```bash
sudo tar xpf ${L4T_RELEASE_PACKAGE = the L4T Package }
cd Linux_for_Tegra/rootfs/
sudo tar xpf ../../${SAMPLE_FS_PACKAGE = The Sample File System}
cd ..
sudo ./apply_binaries.sh
```
3. After running apply_binaries.sh, put your jetson kit into "USB Recovery Mode".
4. Now run the flash.sh to flash to install the L4T  on the board:
```bash
sudo ./flash.sh ${Your Developer Kit} mmcblk0p1
```
 After running flash.sh, it may display an error stating "flash.sh requires root privilege". You may have to alter the flash.sh file.
 
In the flash.sh will check if User is root and exit if not, even if you run flash with sudo. You have to alter this line of code to allow you to run flash.sh. The code is on line 828:
![alt text](https://raw.githubusercontent.com/vincentcheng08/Jetson-TX2_Documentation/master/Flashsh_Error.png)

## Install Jetpack for the jetson tx2
### With Ubuntu 
1. Install the SDK manager from [here](https://developer.nvidia.com/embedded/downloads) 
2. Then run this : 
```bashWe
sudo apt install ./sdkmanager-[version].[build#].deb 
```
3. Create an account with either [NVOnline](https://partners.nvidia.com/) and [Developer Zone](https://developer.nvidia.com/)

4. Run the sdk manager and login with your credientials.
![alt text](https://raw.githubusercontent.com/vincentcheng08/Jetson-TX2_Documentation/master/sdkm-login.png)

5. Then set the host machine, target Jetson board , and jetpack.
![alt text](https://raw.githubusercontent.com/vincentcheng08/Jetson-TX2_Documentation/master/sdkm-1-jetson-target-options.png)
6. enter sudo password to allow install.

7. To install SDK input the jetson username and password.

## Install Jetpack 4.2 without Ubuntu 
1. If the Jetpack has been updated, we ran sdk manager and installed the necessary tools kits deb files and repository json. The repository json explains how to install tools onto the board to run cuda and additional features.

2. We provided the deb files for the tools provided in the jetpack 4.2 packages. If you are installing Jetpack 4.2, then use the packages provided here.

3. There is a bash scripts that will install all the repos onto the board. Run the bash script on your board and make sure that deb packages are in your home directory on your board.



## GPU Programming
 Currently, the Jetson TX2 primarily supports CUDA Toolkit that is installed with the Jetpack package. With CUDA, Jetpack include TensorRT,cuDNN(CUDA Deep Neural Network), and VisionWorks.
