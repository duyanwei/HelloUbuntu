# Install Ubuntu 20.04 alongside with Windows 10 and Ubuntu 16.04

## 1. Background

I plan to install ubuntu 20.04 on a new M.2 SSD drive, and the computer already has Windows 10 and Ubuntu 16.04 installed on a second SSD. In order to do that, a ```/boot``` space for the new ubuntu system needs to be installed on the same disk with windows, so that it can be boosted properly.

BTW, for those whose compute does not support M.2 SSD, get a adapter (M.2 NVME PCIe 3.0 x4 Adapter)

## 2. Main Step


### 2.1 Partition

#### Shrink Windows system
- Usually it is easy to shrink the windows system of certain size(mine is 2GB) for unallocated space, where the ```/boot``` of the new ubuntu system would be installed.

- Useful link:
    - [Win10 + Ubuntu16.04/Ubuntu18.04](https://blog.csdn.net/qq_24624539/article/details/81775635)
    - [Ubuntu16.04 + Win10](https://blog.csdn.net/fesdgasdgasdg/article/details/54183577)

#### Shrink Windows system in the installed Ubuntu
- Since the Windows system is not accessible for some reason  (PW missing), one could recover the windows with a new PW by a bootable USB drive, more details can be found on microsoft.com. I chose to use [**gparted**](https://gparted.org/) and get this job done in the installed Ubuntu 16.04 system.

- After logging the old ubuntu 16.04 system, install gparted with ```sudo apt install gparted ```

- Resize the disk where the windows system is installed (you cannot resize ubuntu system, which is being used now)

- Useful link:
    - [gparted official FAQ](https://gparted.org/faq.php)
    - [ask Ubuntu](https://askubuntu.com/questions/1030508/can-i-safely-resize-windows-10-system-partition-from-ubuntu)

### 2.2 Install Ubuntu 20.04

#### Partition

#### Boot
- Create `/boot` as logic, choose the allocated space from **the original SSD**.

- Create `/root` as logic, ext4

- Create `/swap` as logic (mine is 8GB)

- Create `/home` as logic, ext4

- Useful link:
    - [Win10 + Ubuntu16.04/Ubuntu18.04](https://blog.csdn.net/qq_24624539/article/details/81775635)

#### Warning about EFI
- After the `partition` part is done, when clicked `install` button, there is a popped error message ***that warns about the missing partition of EFI and it may cause the ubuntu system un-bootable.*** It looks scary and still lets you continue. 

- The solution varies, some say just allocate a space around 500MB, some suggest that if the computer has windows installed, it is not necessary to create extra space for it, so I clicked continue and move forward all the way down.

- Useful link:
    - [ask Ubuntu](https://askubuntu.com/questions/1144552/dual-boot-no-efi-system-partition-was-found)

### 2.3 Add new Ubuntu system to the boot menu

- When the installation is done, restart the computer and don't forget to unplug the usb-drive.

- For the first time, I did NOT see Ubuntu 20.04 in the boot menu, I logged in the Ubuntu 16.04 system and updated the `grup` with `sudo update-grub2`. And then it appears on the boot menu.

- Useful link:
    - [Windows + two Ubuntu systems](https://blog.csdn.net/weixin_30797199/article/details/95826744)

### 2.4 Change boot order
-  ```sudo vim /etc/default/grub``` 
- set ``` GRUB_DEFAULT ```
- ```sudo update-grup ```

## 3. Configure Ubuntu

### Change Window Title-bar buttons
- ``` sudo apt install gnome-tweaks```

### 


## 4. Install 3rdparty libraies

### vim
- install [vim](https://github.com/duyanwei/k-vim/tree/yw/vim), branch `yw/vim`