# Installing Armbian Linux on Vontar X3 (or other s905 devices)

This is how i installed Armbian on vontar x3 TV box. To use it as a linux server (or mini pc).

I hope this will help you 



## What do you need

- A Vontar X3 box (or any box having arm like S905 cpu ...)
- SD CARD (at least 16 GB)
- one toothpick

- Rufus

## Burn the image on the sd card with Rufus 

I used image from https://github.com/ophub/amlogic-s9xxx-armbian

This repo propose only server images, for desktop image, look here : https://github.com/armbian/community/releases

You can choose ubuntu or debian based image, 
I choosed debian based, and i pick the image for s905x3 (the cpu of Vontar-x3).
So i picked this image : Armbian_24.11.0_amlogic_s905x3_bookworm_6.6.62_server_2024.11.20.img.gz

## Prepare the boot on sd card

### u-boot

Depending on your cpu you need to set the u-boot.ext

Find your corresponding files [here](https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/build-armbian/armbian-files/common-files/etc/model_database.conf)

For Vontar x3, you have a s905x3, and you need u-boot-s905x2-s922 or u-boot-s905x3 

Rename u-boot-s905x2-s922.bin to u-boot.ext 

### Device tree block 

For Vontar X3, you need this dtb file : meson-sm1-hk1box-vontar-x3.dtb.

For other devices, you can again fin your corresponding files [here](https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/build-armbian/armbian-files/common-files/etc/model_database.conf).
If your device is not listed inside, you can try one dtb file that has same CPU, RAM memory, and same ethernet speed 

In extlinux dir, copy extlinux.conf.bak to extlinux.conf

Then edit the fdt line, for example :

    fdt /dtb/amlogic/meson-sm1-hk1box-vontar-x3.dtb

Do the same in uEnv.txt (i am not sure of this, but just in case)

## Boot on the sd card 

- Unplug your vontar x3
- Plug a screen with HDMI cable, to see what is going on
- Insert the SD card
- Use the toothpick to press the reset button, it should be inside the audio jack port
- Hold the button while you plug the power 

If this is not the correct dtb file, it will be stuck at "starting linux kernel". So try another one.

Then linux will start to boot on the sd card. You can plug an ethernet cable, and ssh to it (user : root, password: 1234, port: 22)

## Install on eMMC

You can install on the eMMC (inside memory) to have faster disk speed.
But be careful, it may brick your device, and you will lose access to the android firmware. 

Run : 

    armbian-install -m yes -a no

Enjoy your cheap linux server now ! 


## Performance benchmark

(todo)


