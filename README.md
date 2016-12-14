# How-to-compile-kernel-module
How to compile a kernel module with/for another kernel

1- Download and Extract Android NDK.  
2- Download desired module source.  
3- Create Makefile with below content:  
```javascript
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 29
EXTRAVERSION =

obj-m := cpufreq_smartass.o
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
