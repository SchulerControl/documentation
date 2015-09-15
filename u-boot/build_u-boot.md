##Build u-boot bootloader
You need to have completed all steps of the setup tutorial before continuing with this one.

If you like to build u-boot from scratch, want to try a different version or do some changes to the configuration you should start from the beginning of this tutorial. If you just want to compile the provided u-boot you could also clone the following repository (https://github.com/SchulerControl/u-boot) and jump to **Configure and compile u-boot**.


###Clone u-boot from denx.de:
The bootloader used in all SchulerControl devices is u-boot with support in mainline u-boot. All what's needed additionally are two files to enable support for ext4 filesystems and the pre-configured u-boot environment. Your current terminal directory shoud be 'scdevice'.

>```
$ git clone git://git.denx.de/u-boot.git u-boot/
$ cd u-boot
```

###Switch to new branch u-boot version v2014.10:
This version is used in our production devices and it is proven to work. You might want to try a newer version if you're adventurus (and we'd love to hear from you how it worked out!). This command creates a new branch of that specific version in git and switches to it.

>```
$ git checkout -b sc_sps_1_v2014.10 v2014.10
```

###Apply files for ext4 support and u-boot environment
We need to get two files for u-boot to work correctly with our devices and copy the previously downloaded files into our u-boot directory (downloaded in setup tutorial from https://github.com/SchulerControl/additional_files.git). 

>```
$ cp ../additional_files/sc_sps_1.h include/configs/sc_sps_1.h
$ cp ../additional_files/env.txt env.txt
```

###Configure and compile u-boot:
Now is the time to configure u-boot for our device and compile some needed tools and u-boot itself.

>```
$ make sc_sps_1_config
$ make all
$ make u-boot.sb
```

###Make u-boot file bootable on imx28:
Last step is to generate a bootable u-boot file. To do so we use the mxsboot tool compiled before (please watch for the different filenames with trailing 'b' and 'd' as the difference).

>```
$ ./tools/mxsboot sd u-boot.sb u-boot.sd
```

**Congratulations! You just build your first u-boot bootloader for SchulerControl devices!** The file 'scdevice/u-boot/u-boot.sd' is your new u-boot which we will include later into our root filesystem.


###Generate u-boot environment
u-boot needs a special enviornment file which we generate with the following command.

>```
$ cat env.txt | ./tools/mkenvimage -s 16384 -o env.img
```

The file 'scdevice/u-boot/env.img' is the compiled u-boot environment used later in the root filesystem.

