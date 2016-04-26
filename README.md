#exfat-synology
##Perfectly mount/unmount exfat disk partition on Synology DiskStation NAS (x86 platform)

#How-To Create Manual Mount & Unmount Control
1.On Synology DiskStation WebUI, go to [Control Panel] -> [Terminal & SNMP] -> [Enable Telnet service];
![image](https://raw.githubusercontent.com/luckylz2git/exfat-synology/master/images/create_mount_point.png/enable_telnet.png)

2.Go to [Control Panel] -> [Shared Folder], and create a dummy shared folder as exfat mount point, e.g. /volume1/usbexfat/;

3.Put anything inside shared folder usbexfat, to indicate the unmount status, e.g. a blank file named: exfat_usb_device_unmounted;

4.Download this repository zip files and extract to any available directory on your NAS, e.g. /volume1/files/exfat-synology-master/;

5.Use telnet login your NAS as root, and run the following commands:

filepath=/volume1/files/exfat-synology-master/ && chmod 755 $filepath/install.sh && $filepath/install.sh $filepath

6.Go back to [Control Panel] -> [Task Scheduler], create [User-defined script] for mount & unmount, un-check the [Enabled] and change [Schedule] tab to [Run on the following date] -> [Do not repeat]:

mount & unmount script usage:
/usr/local/exfat-synology/exfat.sh [mount|unmount] [login] [password] [path/to/mount/point]

example:
/usr/local/exfat-synology/exfat.sh mount root 12345 /volume1/usbexfat/
/usr/local/exfat-synology/exfat.sh unmount root 12345 /volume1/usbexfat/

7.Manual mount exfat partition, plug-in the USB device, run the task mount exfat in the [Task Scheduler];

8.Manual unmount exfat partition, close all file station or any telnet connection which access to the mount partition, run the task unmount exfat in the [Task Scheduler];

9.Go to [Control Panel] -> [External Devices], to eject the USB device;

#How-To Create Automatic Mount Control

/opt/bin/mtelnet.sh mount root mis-sech /volume1/exfat/