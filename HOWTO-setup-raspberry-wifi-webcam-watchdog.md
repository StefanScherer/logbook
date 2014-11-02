# HowTo setup a watchdog for your heat pump

## Parts

* RaspberryPi
* Edimax WiFi
* Webcam 
* LED light

## Setup WiFi

Followed instructions in [How-To: Add WiFi to the Raspberry Pi](http://raspberrypihq.com/how-to-add-wifi-to-the-raspberry-pi/) and [Raspberry Pi – WLAN einrichten (Edimax)](http://www.datenreise.de/raspberry-pi-wlan-einrichten-edimax/)

```bash
dmesg | more
sudo vi /etc/network/interfaces
```

contents

```
auto lo
iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
auto wlan0

iface wlan0 inet dhcp
   wpa-ssid "Your Network SSID"
   wpa-psk "Your Password"
```

Edit you SSID and PSK and save the file.

```bash
sudo service networking reload
ifconfig
```

## Setup Camera

The LifeCam HD-3000 works out of the box, so I only need some tools to take pictures.
Followed the instructions at [
Timelapse movie with Raspberry Pi and fswebcam](http://martin-denizet.com/timelapse-movie-with-raspberry-pi/).

```bash
sudo apt-get update
sudo apt-get install fswebcam
```

config file `/home/pi/code/watchdog/fswebcam.conf`

```
device /dev/video0
resolution 1280x720
no-banner
jpeg 90
loop 30
background
save /home/pi/code/watchdog/images/last.jpg
delay 1
skip 30
```

rename script `/home/pi/code/watchdog/rename.sh`

```bash
#!/bin/sh
DATE=`date -u +"%Y-%m-%dT%H-%M-%SZ"`.jpg
mv /home/pi/code/watchdog/images/last.jpg /home/pi/code/watchdog/images/$DATE
```

start script

```bash
#!/bin/sh
fswebcam -c /home/pi/code/watchdog/fswebcam.conf --exec /home/pi/code/watchdog/rename.sh
```

stop script

```bash
#!/bin/sh
killall fswebcam
```

image folder

```bash
mkdir /home/pi/code/watchdog/images
```



## Next steps

* [Basic Image Processing](https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/robot/image_processing/)
* [Blob Detection](https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/robot/blob_detection/)

