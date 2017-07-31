# Hackintosh z270i 7700k 960EVO installation

This is a collection of notes that i use to install macOS, this is not a tutorial.

Motherboard: ASUS ROG Strix Z270I

CPU: Intel i7-7700k

SSD: Samsung NVMe SSD 960EVO

OS: macOS Sierra 10.12.5 (can be updated to 10.12.16)

## Tips that can speed up the process:
- 32GB USB sticks are generally faster than 16GB ones
- You can boot from the USB by pressing F7 at the boot logo, but i prefer to edit the BIOS settings
- 

## 1. Installation
-Create an USB 2.0 stick with Unibeast o similar, and edit the config.plist as following
 - Add FakeCPUID
 - Add IntelIGFX
 - Add NVMEpatches under KextToLoad

or download ___

- Boot from the USB stick
- Press Continue and select Disk Utility from the menu bar
- Format the disk
- Install macOS Sierra
- After the installation update the system to 10.12.16 if you want

## 2. Post-installation
- Download https://github.com/RehabMan/patch-nvme/archive/master.zip
- Run the command ./patch_nvme.sh 10_12_6 inside the unzipped folder 
- Delete /S/L/E/IONVMeFamily.kext
- Install the generated HackNVMe... .kext with kextwizard http://wizards.osxlatitude.com/kext/download.html and clean the kext cache	
(the order of the steps matters!)
- Unmount all EFI partitions
- Download multibeast https://www.tonymacx86.com/resources/multibeast-sierra-9-1-0.334/
- Make sure that it is on the main drive
- Select the following options:
[img ...]
-Reboot	
	
## Useful commands:
```
diskutil list
diskutil mount <partition eg. /dev/disk0s0>
diskutil mount -mountPoint <mount point eg. /Volumes/EFIUSB/> <source partition eg. /dev/disk0s2>
diskutil mountDisk <disk eg. /dev/disk0>


touch /System/Library/Extensions && kextcache -u / # specify the macOS installation path
```



