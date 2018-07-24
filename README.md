# amifldrv source code

This is the source code for the `amifldrv` kernel module used by the AMI
Aptio flashing tool for linux, `afulnx` or the HP fork `safulnx2`.

All of the AMIs BIOS flash tools bring their own version of the driver,
trying to compile it in the background which on most systems fails because
the kernel is much newer, compile options are broken or the tool/driver does
not match the kernel.

Originally the 32 Bit flash tools like `safulnx2` or `afulnx` needed a 32 Bit
kernel as structures passed by ioctl had no conversion. 

This repository contains some fixes to let `safulnx2` be partially used on a
64 Bit Kernel on a HP t620

An original dump of the sourcecode of the corresponding tool can be 
retrieved by running the flash tool, pressing CTRL-Z and looking into
the `.temp` directory. 

This repo is a fork of Roman Hargraves https://github.com/RomanHargrave/amifldrv

# Compatibility

Using the `safulnx2` from the original HP ThinPro 5/6/7 lets one dump
the original ROM contents.

# Usage

Clone this repository and build the driver by running make - You will need
build essentials and your matching kernels headers available.

Then while in the build directory issue a 

    ln -s amifldrv_mod.ko amifldrv_mod
    ln -s amifldrv_mod.ko amifldrv_mod.o

Then run the appropriate flash util while in that diretory:

    root@ubuntu:~/amifldrv# /root/safulnx2 /s
    cp: './amifldrv_mod.o' and './amifldrv_mod' are the same file
    +---------------------------------------------------------------------------+
    |                 AMI Firmware Update Utility  v1.02_HP                     |
    |      Copyright (C)2012 American Megatrends Inc. All Rights Reserved.      |
    +---------------------------------------------------------------------------+
     Reading flash ............... done                
     - System ROM ID = L40_0205
     - System ROM GUID = 8f1c6dfc-3b1c-41af-ad2ddec6544a6ee8
     - System ROM Secure Flash = Diable.

Flash a new BIOS:

    root@ubuntu:~/amifldrv# /root/safulnx2 ../L40_0214.bin /b /p  
    +---------------------------------------------------------------------------+
    |                 AMI Firmware Update Utility  v1.02_HP                     |
    |      Copyright (C)2012 American Megatrends Inc. All Rights Reserved.      |
    +---------------------------------------------------------------------------+
    
     Reading flash ............... done                
     - FFS checksums ......... ok
     Erasing Boot Block .......... done                
     Updating Boot Block ......... 0x007B6C00 (77%) 
     Updating Boot Block ......... done                
     Verifying Boot Block ........ done                
     Erasing Main Block .......... done                
     Updating Main Block ......... 0x0012C000 (10%) 
     Updating Main Block ......... done                
     Verifying Main Block ........ done       

# safulnx2

`safulnx2` was shipped with HP ThinPro - You will need to dissect their
filesystem image to get the binary:

    wget ftp://ftp.hp.com/pub/tcdebian/OSImages/Z7X70015.dd.gz
    gzip -d Z7X70015.dd.gz
    sudo kpartx -a Z7X70015.dd
    sudo mount /dev/mapper/loop0p2 /media/cdrom
    sudo cp /media/cdrom/root/usr/sbin/safulnx2 .

# License issues

AMI _did not_ specify a license for this code in `readme.txt`,
`readme_afulnx.txt` or any other file, including the source code.
Furthermore, Linux kernel modules can be considered derivitave works of
the Linux kernel, which is licensed under the GNU General Public License.
The GPL _mandates_ that source code be made available. AMI appear to have
gone out of their way to make obtaining the _full_ module source rather
obfuse, as the tool that emits it will delete it immediately after
exiting.

I do not claim any ownership of this code.


