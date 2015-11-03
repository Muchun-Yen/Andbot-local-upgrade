# Andbot-local-upgrade

# Introduction

The Andbot auto upgrade OTA (A-OTA) architecture include 3 parts; the Andbot app, cloud server, and upgrade system.
For the local upgrade, we will just discuss "the upgrade system" part in A-OTA architecture.

The Andbot system can install in SD card or eMMC. (The capacity should be more than 8GB )

This document describes how to make a Andbot system in SD card.
<You can use the same way to make an Andbot system in eMMC.>

#### There are 2 types of binary images for Andbot system SD card
* #### Full SD card binary image. 
	* It compresses an Andbot system SD card to an image. 
	* It is used to recover an Andbot system card or make it from a new SD card.
	* The file name format is  [release data]-[minimum capacity]-[storage device]¡¨.img.gz¡¨ (ex. 20151102-8g-sdcard.img.gz).

* #### Upgrade partition binary image.
	* It compresses Andbot rootfs partition(trusty) to an image.
	* It is used to upgrade the trusty partition.
	* The file name format is [release date]-¡§trusty.img.gz¡¨ (ex. 20151102-trusty.img.gz)
		

# Full SD card binary image.

An Andbot system SD card format shows as this diagram.
![SDcard partitions](https://docs.google.com/drawings/d/1yWVKoBfOmzN5G0ehQm-baXEqNDuhX32Q_PMMvmwtMic/pub?w=629&h=650)

We provide a basic binary system image which store in the "Simple Storage Server (S3)" in Amazon Web Services (AWS).

#### Download the basic system binary image
Engineer can download the basic binary system file 20151102-8g-sdcard.img.gz (https://s3-us-west-2.amazonaws.com/andbot/20151102-8g-sdcard.img.gz)

#### More than 8G bytes Micro SD card.   
For make an Andbot system SD card. You have to prepare a micro SD card which unless 8G byte.

#### dd command to converting and formatting according to the SD card.

##### <<Warning:  the SD card will be formatted and converted for Andbot system>>

```javascript
$ sudo -s
$ gzip -dc 20151102-8g-sdcard.img.gz | dd of=/dev/sdb bs=1M
```

After the process finished, the Andbot basic system SD card is ready to use.

# The upgrade binary image and related boot files for Andbot

We provide some system upgrade binary images in AWS S3 server. You can use those images to upgrade Andbot system in local.

In the most case, you have not to upgrade the BOOT files (which are u-boot, HW dtb, kernel, and uInitrd).Unless you want to upgrade them.

The upgrade partitions;the BOOT and trusty partitions diagram shows as the diagram
![upgrade partition] (https://docs.google.com/drawings/d/1s72u6AeK68l58Sm4Pvh-Ni_Fyf29bVpfP3Vdk6rSwi0/pub?w=680&h=630) 

#### if you want to upgrade the BOOT files, you can just replace those files in BOOT.
boot.ini	(https://s3-us-west-2.amazonaws.com/andbot/boot.ini)

exynos5422-odroidxu3.dtb	(https://s3-us-west-2.amazonaws.com/andbot/exynos5422-odroidxu3.dtb)

uInitrd	(https://s3-us-west-2.amazonaws.com/andbot/uInitrd)

zImage	(https://s3-us-west-2.amazonaws.com/andbot/zImage)


#### Download the upgrade system binary image
There is a upgrade system in (https://s3-us-west-2.amazonaws.com/andbot/20151102_trusty.img.gz)

#### dd command to converting and formatting according to the sdcard.(change the image name to trusty.img.gz)

```javascript
$ sudo -s
$ gzip -dc trusty.img.gz | dd of=/dev/sdb2 bs=1M
``` 

After the process finished, reboot the system for useing the new version on the Andbot.

# Reference
* Andbot auto upgrade OTA (A-OTA)
	* https://github.com/Muchun-Yen/Andbot-Auto-Upgrade-OTA

* ODROID-XU3 EVM board 
	* http://www.hardkernel.com/main/products/prdt_info.php?g_code=G140448267127	

* Amazon Web Services
	* https://aws.amazon.com
