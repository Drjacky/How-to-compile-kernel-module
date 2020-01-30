# How to compile kernel module
How to compile a kernel module with/for another kernel

1- Download and Extract Android NDK(for example: http://mirrors.neusoft.edu.cn/android/repository/android-ndk-r13b-linux-x86_64.zip).  
2- Download desired module source.  
3- Create Makefile with below content:  
```javascript
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 29
EXTRAVERSION =

obj-m := module_sourcecode.o
PWD := $(shell pwd)
default:
        $(MAKE) ARCH=arm CROSS_COMPILE=/home/path/to/androidnsk/android_platform/prebuilt/linux-x86/toolchain/arm-eabi-4.4.3/bin/arm-eabi- -C $(KERNEL_DIR) SUBDIRS=$(PWD) modules
clean:
        $(MAKE) -C $(KERNEL_DIR) SUBDIRS=$(PWD) clean
```
4- Execute ```make``` command.

A simple hello world kernel module:  
```javascript
#include <linux/module.h>  /* Needed by all modules */
#include <linux/kernel.h>  /* Needed for KERN_ALERT */

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Drjacky, 2016");
MODULE_DESCRIPTION("Demo module");

int init_module(void){
   printk("<1>Hello World\n");

   // A non 0 return means init_module failed; module can't be loaded.
   return 0;
}
```

Note (Optional):  
Add these helpful lines for all the times, to your .bashrc file:  
```javascript
export ANDROID_NDK=/home/drjacky/Desktop/DLz/android-ndk-r10e
export ANDROID_NDK_ROOT=/home/drjacky/Desktop/DLz/android-ndk-r10e
export ANDROID_SDK=/home/drjacky/Desktop/DLz/android-sdk-linux
export NDK=/home/drjacky/Desktop/DLz/android-ndk-r10e
export ANDROID_API_VERSION=android-14
export NDK_SYSROOT=/home/drjacky/Desktop/DLz/android-ndk-r10e/platforms/android-14/arch-arm
export TOOLCHAIN=/home/drjacky/Desktop/DLz/android-ndk-r10e/toolchains/arm-linux-androideabi-4.8/prebuilt/linux-x86_64
export ANDROID_TOOLCHAIN=/home/drjacky/Desktop/DLz/android-ndk-r10e/toolchains/arm-linux-androideabi-4.8/prebuilt/linux-x86_64
export adb=/home/drjacky/Desktop/DLz/android-sdk-linux/platform-tools
export android=/home/drjacky/Desktop/DLz/android-sdk-linux/tools
#export ndk-build=/home/drjacky/Desktop/DLz/android-ndk-r10e
```
And these to your /etc/environment file:  
```javascript
ANDROID_NDK="/home/drjacky/Desktop/DLz/android-ndk-r10e"
ANDROID_SDK="/home/drjacky/Desktop/DLz/android-sdk-linux"
NDK="/home/drjacky/Desktop/DLz/android-ndk-r10e"
ANDROID_API_VERSION="android-14"
export NDK_SYSROOT="/home/drjacky/Desktop/DLz/android-ndk-r10e/platforms/android-14/arch-arm"
TOOLCHAIN="/home/drjacky/Desktop/DLz/android-ndk-r10e/toolchains/arm-linux-androideabi-4.8/prebuilt/linux-x86_64"
adb="/home/drjacky/Desktop/DLz/android-sdk-linux/platform-tools"
android="/home/drjacky/Desktop/DLz/android-sdk-linux/tools"
##ndk-build="/home/drjacky/Desktop/DLz/android-ndk-r10e"
```
