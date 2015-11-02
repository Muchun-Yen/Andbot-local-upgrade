# Andbot-local-upgrade

# Introduction

The Andbot auto upgrade OTA (A-OTA) architecture include 3 parts; the Andbot app, colud server, and upgrade system.
for the local upgrade, we will just discussion "the upgrade system" part in A-OTA architecture.

# A basic binary image for Andbot

Andbot is developed on Odroid XU3 board. The basic binary image is for all the HW components and file systems caould be operating well.


We provide a basic binary system image which store in the "Simple Storage Server (S3)" in Amazon Web Services (AWS).

#### Download the basic system binary image
Engineer can download the basic binary system file 20151102-8g-sdcard.img.gz (https://s3-us-west-2.amazonaws.com/andbot/20151102-8g-sdcard.img.gz)

#### More then 8G bytes Micro SD card.   
For build up the basic Andbot system. you have to prepare a micro SD card which unless 8G byte.

#### dd command to converting and formatting according to the sdcard.

##### Warning : the SD card will be formatted and converted for Andbot systemfor Andbot system

```javascript
$ sudo -s
$ gzip -dc 20151102-8g-sdcard.img.gz | dd of=/dev/sdb bs=1M
```

After the process finished, the Andbot basic system is ready to use.

# The upgrade binary image and related boot files for Andbot
We prove some system upgrade binary images in AWS S3 server. you can use the images to upgrad system in local.
In the most case, you have not to upgrade the BOOT files (which are u-boot,HW dtb,kernel, and uInitrd).Unless you upgrade them.

The upgrade partitions; the BOOT and trusty partitions
![upgrade partition] (https://docs.google.com/drawings/d/1s72u6AeK68l58Sm4Pvh-Ni_Fyf29bVpfP3Vdk6rSwi0/pub?w=680&h=630) 

#### if you want to upgrade the BOOT files, you can just replace those files in BOOT.
boot.ini	(https://s3-us-west-2.amazonaws.com/andbot/boot.ini)

exynos5422-odroidxu3.dtb	(https://s3-us-west-2.amazonaws.com/andbot/exynos5422-odroidxu3.dtb)

uInitrd	(https://s3-us-west-2.amazonaws.com/andbot/uInitrd)

zImage	(https://s3-us-west-2.amazonaws.com/andbot/zImage)


#### Download the upgrade system binary image
There is a upgrade system in (https://s3-us-west-2.amazonaws.com/andbot/20151102_trusty.img.gz)

#### dd command to converting and formatting according to the sdcard.

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