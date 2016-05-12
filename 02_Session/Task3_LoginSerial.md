## 0. Info
- Protocol: Session 02_Task3
- Date: 10.05.2016
- Time: 09:00 - 16:00
- Topic: Login Serial

## 1. Setup
By the hint of one colleague I followed the tutorial from <http://www.miklor.com/COM/UV_Drivers.php#install> to install the right driver. Since the newest driver is not working I needed to downgrade to the driver `v3.2.0.0`. With the following configuration I was able to connect to the raspberry over serial cable.
I connected the console cable to the following pins:

- VCC -> RPi Pin 02 (DC Power 5V, Red)
- GND → RPi Pin 06 (Ground, Black)
- RXD → RPi Pin 08 (TX, White)
- TXD → RPi Pin 10 (RX, Green)

![Image of connection by serial cable http://madner.eu/mcm/pics/02_03_SerialCable.jpg](http://madner.eu/mcm/pics/02_03_SerialCable.jpg "Setup Serial Cable")

With the following settings in putty I was able to connect to the raspberry by serial connection:

![Image of setup serial connection http://madner.eu/mcm/pics/02_03_SetupPutty.jpg](http://madner.eu/mcm/pics/02_03_SetupPutty.jpg "Setup Serial Connection in Putty")