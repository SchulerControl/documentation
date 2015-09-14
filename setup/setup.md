##Pre-requisites when building your own u-boot bootloader and linux kernel

###How to read the tutorials:
Terminal commands are marked by a '$' (dollar) sign. You can type these command or copy them into your terminal (without the dollar sign).


###Setup your build system:
First we need to install some general development tools needed for Ubuntu 14.04 LTS (64-bit). If you're using a different operating system please see http://kernelnewbies.org/KernelBuild for more information.

>```
$ sudo apt-get install libncurses5-dev gcc make git exuberant-ctags bc libssl-dev
```

###Let's get started:
Let's start with a new directory where everything will happen from now on!

>```
$ mkdir scdevice
$ cd scdevice
```

###Download and setup a cross-compiler:
To compile for ARM we need a cross compiler. We will use the recent ELDK cross-compiler from Denx for this tutorial. You can use a different cross-compiler if you like, but please be reminded that you will probably need to change some path/commands here and there. More in-depth information about the setup and installation of ELDK can be found at http://www.denx.de/wiki/ELDK-5/

>```
$ wget ftp://ftp.denx.de/pub/eldk/5.6/targets/armv5te/eldk-eglibc-i686-arm-toolchain-5.6.sh
$ chmod +x eldk-eglibc-i686-arm-toolchain-5.6.sh
```

Start the installer and press enter twice to install into default directory (/opt/eldk-5.6/armv5te). Enter your password when prompted and ELDK will be extracted into the chosen directory.

>```
$ ./eldk-eglibc-i686-arm-toolchain-5.6.sh
```

We will compile for ARM (armv5te) and therefor need to export some environment variables of ELDK (or different cross-compiler) into your terminal. To to so copy and paste all lines from the file '/opt/eldk-5.6/armv5te/environment-setup-armv5te-linux-gnueabi' into your terminal.

![ELDK environment variables](https://github.com/SchulerControl/documentation/setup/images/eldk_environment_variables.png)


###Download additionally needed files
To use the u-boot bootloader and linux kernel with a specific board you need an u-boot environment, a kernel config and device tree file. We will download these files now and apply them later.
>```
$ git clone https://github.com/SchulerControl/additional_files.git
```

Now we have setup our system and are good to go!

