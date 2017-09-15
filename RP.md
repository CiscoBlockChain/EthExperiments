# Raspberry Pi Setup

We are using RP2 model B V1.1

## Flash Drive

The microSD card needs to be flashed to the [latest operating system](https://www.raspberrypi.org/downloads/raspbian/).  We are using stretch for this. 

Following the instructions we stick the SD card into an adapter that in turn goes into the Mac

```
diskutil list

```
Mine shows up as ```/dev/disk2 (internal, physical):```

So we eject the disk: 

```
diskutil unmountDisk /dev/disk2
sudo dd bs=1m if=~/Downloads/2017-09-07-raspbian-stretch.img of=/dev/rdisk2 conv=sync
```
This then can take a few minutes to copy onto the SD card. 

Attach power, keyboard, mouse, and hdmi cable to monitor and start it up. 

* Enable SSH
* Enable camera
* Update the software
```
sudo apt-get update
sudo apt-get upgrade
```
Reboot machine.

## Test Camera

We attached a simple USB camera to the RP2 and followed [these instructions](https://pimylifeup.com/raspberry-pi-webcam-server/) to create a camera monitoring system. 
