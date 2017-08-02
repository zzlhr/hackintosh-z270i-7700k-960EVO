# Hackintosh z270i 7700k 960EVO installation

This is a collection of notes that i use to install macOS, this is not a tutorial.

### Hardware
- Motherboard: ASUS ROG Strix Z270I
- CPU: Intel i7-7700k
- SSD: Samsung NVMe SSD 960EVO
- OS: macOS Sierra 10.12.5 or 10.12.6

### Tips that can speed up the process:
- 32GB USB sticks are generally faster than 16GB ones
- You can boot from the USB by pressing F7 at the boot logo, but i prefer to edit the BIOS settings
- The order of the steps below matters



## 1. Installation
1. Create an USB 2.0 stick with Unibeast o similar, and edit the config.plist as following:
 - Add FakeCPUID 0x0506E3
 - Add IntelGFX 0x19168086
 - Add IONVMeFamily patches under KextToLoad

 or [Downlaod config.plist](https://raw.githubusercontent.com/fttx/hackintosh-z270i-7700k-960EVO/master/config/config.nvme.patch.plist)

2. Boot from the USB stick
3. Press Continue and select Disk Utility from the menu bar
4. Format the disk
5. Install macOS Sierra
6. After the installation update the system to 10.12.16 if you want

## 2. Post-installation
1. Download https://github.com/RehabMan/patch-nvme/archive/master.zip
2. Run the command ./patch_nvme.sh 10_12_6 inside the unzipped folder 
3. Delete /S/L/E/IONVMeFamily.kext
4. Install the generated HackrNVMeFamily-10_12_6.kext with [Kext Beast](https://www.tonymacx86.com/resources/kextbeast-2-0-1.310/) and clean the kext cache
5. Unmount all EFI partitions
6. Download [MultiBeast - Sierra 9.1.0](https://www.tonymacx86.com/resources/multibeast-sierra-9-1-0.334/download?version=155)
7. Make sure that Multibeast is on the main drive
 
 Clover will install a [config.plist](https://raw.githubusercontent.com/fttx/hackintosh-z270i-7700k-960EVO/master/config/config.clover.no.nvme.patch.plist) identical to the one of the step 1.1 except for the IONVMeFamily part and other parts for the new drivers
8. Select the following options:
![multibeast settings](https://raw.githubusercontent.com/fttx/hackintosh-z270i-7700k-960EVO/master/img/multibeast.png "Multibeast settings")
9. Reboot	

To remove the audio humming, lower the Input Gain from the VoodooHDA pref pane.
To make it permanent edit /L/E/VoodooHDA.kext Info.plist, or [download the already edited kext](https://github.com/fttx/hackintosh-z270i-7700k-960EVO/tree/master/kext/VoodooHDA.kext) and install it

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

## Useful links
- [Clover Configurator](http://mackie100projects.altervista.org/download-mac.php?version=classic)
- [Kext Wizard](http://wizards.osxlatitude.com/kext/download.html)
- [MultiBeast - Sierra 9.1.0](https://www.tonymacx86.com/resources/multibeast-sierra-9-1-0.334/download?version=155)
- [Kext Beast](https://www.tonymacx86.com/resources/kextbeast-2-0-1.310/) 
- [patch-nvme](https://github.com/RehabMan/patch-nvme/archive/master.zip)
- [VSCode](https://code.visualstudio.com/docs/?dv=osx)
- [Google Chrome](https://www.google.it/chrome/browser/desktop/index.html)