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
sudo tar xpf ${L4T_RELEASE_PACKAGE}
cd Linux_for_Tegra/rootfs/
sudo tar xpf ../../${SAMPLE_FS_PACKAGE}
cd ..
sudo ./apply_binaries.sh
```
3. After running apply_binaries.sh, put your jetson kit into "USB Recovery Mode".
4. Now run the flash.sh to flash to install the L4T  on the board:
```bash
sudo ./flash.sh ${Your Developer Kit} mmcblk0p1
```
 After running flash.sh, it may display an error stating "flash.sh requires root privilege". You may have to alter the flash.sh file.
 
In the flash.sh will check if User is root and exit if not, even if you run flash with sudo. You have to alter this line of code to allow you to run flash.sh. The code is on line 828.

## GPU Programming
 Currently, the Jetson TX2 primarily supports CUDA Toolkit that is installed with the Jetpack package. With CUDA, Jetpack include TensorRT,cuDNN(CUDA Deep Neural Network), and VisionWorks.
