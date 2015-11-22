LCD MENU PLATE FOR SAINSTSMART 16x2 LCD KEYPAD
==============================================

This is a python menu for SainSmart 16x2 LCD display keypad, it uses Adafruit library to coontrol button and PiMinerInfo class to get cgminer API information.

Options available for this menu are:

- Show Date/Time
- Show available disk space
- Show RaspberryPi temperature
- Show WLAN IP
- Get information for cgminer API
- Show Local IP
- Shutdown raspberry option
- Reboot raspberry option


You must enable I2c on your RaspberryPi to use this plate:

````
sudo raspi-config
````

Now complete the following steps :

````
Select "8 Advanced Options"
Select "A7 I2C"
Select "Yes"
````

The screen will ask if you want the interface to be enabled :

````
Select "Yes"
Select "Ok"
````

The screen will ask if you want the module to be loaded by default :

````
Select "Yes"
````

The screen will state the module will be loaded by default :

````
Select "Ok"
Select "Finish" to return to the command line
````

When you next reboot the I2C module will be loaded. Next we need to edit the modules file using :

````
sudo nano /etc/modules
````

and add the following two lines :

````
i2c-bcm2708
i2c-dev
````

Use CTRL-X, then Y, then RETURN to save the file and exit.


To help debugging and allow the i2c interface to be used within Python we can install "python-smbus" and "i2c-tools" :

````
sudo apt-get update
sudo apt-get install -y python-smbus i2c-tools
````

When you power up or reboot your Pi you can check the i2c module is running by using the following command :

````
lsmod | grep i2c_
````

Once you’ve connected your hardware double check the wiring. Make sure 3.3V is going to the correct pins and you’ve got not short circuits. Power up the Pi and wait for it to boot.

If you’ve got a Model A, B Rev 2 or B+ Pi then type the following command :

````
sudo i2cdetect -y 1
````

If you’ve got an original Model B Rev 1 Pi then type the following command :

````
sudo i2cdetect -y 0
````

Why the difference? Between the Rev 1 and Rev 2 versions of the Pi they changed the signals that went to Pin 3 and Pin 5 on the GPIO header. This changed the device number that needs to be used with I2C from 0 to 1.

I used a Pi 2 Model B with a sensor connected and my output looked like this :


````
pi@raspberrypi ~ $ sudo i2cdetect -y 1
0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: 20 -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
````

This shows that I’ve got one device connected and its address is 0x20 (32 in decimal).


Python library for accessing character LCDs from a Raspberry Pi or BeagleBone Black.

Designed specifically to work with the Adafruit character LCDs ----> https://learn.adafruit.com/character-lcds/overview

For all platforms (Raspberry Pi and Beaglebone Black) make sure you have the following dependencies:

````
sudo apt-get update
sudo apt-get install build-essential python-dev python-smbus python-pip
````

For a Raspberry Pi make sure you have the RPi.GPIO library by executing:

````
sudo pip install RPi.GPIO
````
