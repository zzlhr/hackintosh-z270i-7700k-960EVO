# Hackintosh z270i 7700k 960EVO installation

This is a collection of notes that i use to install macOS, this is not a tutorial.

- Motherboard: ASUS ROG Strix Z270I
- CPU: Intel i7-7700k
- SSD: Samsung NVMe SSD 960EVO
- OS: macOS Sierra 10.12.5 or 10.12.6

## Tips that can speed up the process:
- 32GB USB sticks are generally faster than 16GB ones
- You can boot from the USB by pressing F7 at the boot logo, but i prefer to edit the BIOS settings
- The order of the steps below matters


## 1. Installation
1. Create an USB 2.0 stick with Unibeast o similar, and edit the config.plist as following:
 - Add FakeCPUID 0x0506E3
 - Add IntelGFX 0x19168086
 - Add IONVMeFamily patches under KextToLoad
 [Downlaod config.plist](raw/master/config/config.nvme.patch.plist)

2. Boot from the USB stick
3. Press Continue and select Disk Utility from the menu bar
4. Format the disk
5. Install macOS Sierra
6. After the installation update the system to 10.12.16 if you want

## 2. Post-installation
1. Download https://github.com/RehabMan/patch-nvme/archive/master.zip
2. Run the command ./patch_nvme.sh 10_12_6 inside the unzipped folder 
3. Delete /S/L/E/IONVMeFamily.kext
4. Install the generated HackrNVMeFamily-10_12_6.kext with [Kext Wizard](http://wizards.osxlatitude.com/kext/download.html) and clean the kext cache
5. Unmount all EFI partitions
6. Download [MultiBeast - Sierra 9.1.0](https://www.tonymacx86.com/resources/multibeast-sierra-9-1-0.334/download?version=155)
7. Make sure that Multibeast is on the main drive
8. Select the following options:
![multibeast settings](raw/master/img/multibeast.png "Multibeast settings")
9. Reboot	


## Useful commands:

### Mount disks and partitions
```
diskutil list
diskutil mount <partition eg. /dev/disk0s0>
diskutil mount -mountPoint <mount point eg. /Volumes/EFIUSB/> <source partition eg. /dev/disk0s2>
diskutil mountDisk <disk eg. /dev/disk0>
```

### Clean cache
```
touch /System/Library/Extensions && kextcache -u / # specify the macOS installation path
```
