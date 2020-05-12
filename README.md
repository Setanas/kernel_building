# Kernel building

Repository for kernel building of a Raspberry pi 4


## Building Raspberry Kernel from sources

I have mainly follow this link to build the kernel from source: 
https://www.raspberrypi.org/documentation/linux/kernel/building.md

To clone the source file of the kernel, I used this command:
```
git clone --depth=1 https://github.com/raspberrypi/linux
```

Then after I have cloned the repository:
```
cd linux
KERNEL=kernel7l
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs
```
I set a variable bash KERNEL to kernel7l which is the image name used for raspberry pi 4 which is where I will try my image.
Then I compile the source thanks to the makefile.


## Installation onto the SD card
All the files needed to install the kernel on the sd card are here in this repository

To do so please mount the boot partition and the root partition of the sd card.

If you want to save your old kernel you can do this:
```
sudo cp {PATH_TO_BOOT_PARTITION}/kernel7l.img {PATH_TO_BOOT_PARTITION}/kernel7l-backup.img
```

Then:

```
sudo cp kernell7l.img {PATH_TO_BOOT_PARTITION}/kernel7l.img
sudo cp dts/*.dtb {PATH_TO_BOOT_PARTITION}/
sudo cp dts/overlays/*.dtb* {PATH_TO_BOOT_PARTITION}/overlays/
sudo cp/dts/overlays/README {PATH_TO_BOOT_PARTITION}/overlays/
```
Before launching we need to add some module in the root partition
```
sudo cp -r 4.19.122-v7l+ {PATH_TO_ROOT_PARTITION}/lib/modules/
```
## Results

Old kernel:

Raspbian booting inside Qemu
![Raspberry pi before](https://github.com/Setanas/kernel_building/blob/master/pictures/before.jpg)

New kernel (after installing):

![Raspberry pi after](https://github.com/Setanas/kernel_building/blob/master/pictures/after.jpg)