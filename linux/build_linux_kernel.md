##Build linux kernel
You need to have completed all steps of the setup tutorial before continuing with this one.

If you like to build the linux kernel from scratch, want to try a different version or do some changes to the configuration you should start from the beginning of this tutorial. If you just want to compile the provided kernel you could also clone the following repository (https://github.com/SchulerControl/linux) and jump to **Build kernel**.


###Get kernel sources from kernel.org:
Good thing is that we use mainline linux kernel sources for all SchulerControl devices! All device drivers and peripheral will just work with the provided kernel config and device-tree file. Cloning the  sources from the official website can take a while, you might want to grab a coffee! Your current terminal directory shoud be 'scdevice'.

>```
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git
$ cd linux-stable
```

###Switch to new branch kernel version v3.10.79:
This long-term-release stable kernel branch is used in our production devices and it is proven to work. You might want to try a newer kernel if you're adventurus (and we'd love to hear from you how it worked out!). This command creates a new branch of that specific version in git and switches to it.

>```
$ git checkout -b sc_mxs_v3.10.79 v3.10.79
```


###Apply specific kernel config and device tree
The provided kernel config is configured to support all device drivers including some WiFi USB sticks and the recent systemd init system. We copy the previously downloaded files into our linux kernel directory (downloaded in setup tutorial from https://github.com/SchulerControl/additional_files.git).

>```
$ cp ../additional_files/sc_sps1_mxs.config .config
$ cp ../additional_files/imx28-sps1.dts arch/arm/boot/dts/imx28-sps1.dts
```

###Make changes to config (optional):
If you like to and know what you are doing, now would be a good time to make some changes in the kernel config. This is for experts only and is NOT NEEDED if you just want to get SchulerControl devices to work! Note: We recommend to use two terminal windows, one for menuconfig and one for the actual kernel build. Be sure to set your current directory in both terminals to 'scdevice/linux-stable'. In the second terminal window type this command to start the kernel menuconfig.

>```
$ make ARCH=arm menuconfig
```

###Build kernel:
Now is the time to actually build the kernel!. Use might want to use the option -jX (with X = number of cores + 1) to speed up the build process. For example, a quad core processor contains four logical cores plus one (4 + 1):

>```
$ make -j5 LOADADDR=0x40008000 uImage
```

![Kernel build result](https://github.com/SchulerControl/documentation/blob/master/linux/images/kernel_build_result.png)


**Congratulations! You just build your first kernel for SchulerControl devices!** The file 'arch/arm/boot/uImage' is your new kernel which we will include later into our root filesystem.

###Build device tree file
The last step is to build the specific kernel device tree file for our devices.

>```
$ make imx28-sps1.dtb
```

The file 'arch/arm/boot/dts/imx28-sps1.dtb' is the binary device tree file which we will include later into our root filesystem.

Copy 'arch/arm/boot/uImage' and 'arch/arm/boot/dts/imx28-sps1.dtb' into a separate directory for later use.

