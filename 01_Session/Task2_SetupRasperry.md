## 0. Info
- Protocol: Session 01_Task2
- Date: 10.05.2016
- Time: 09:00 - 16:00
- Topic: Setup Raspberry Pi and control a LED
## 1. Setting Up Raspberry
First we flashed Minibian (https://minibianpi.wordpress.com/) on the memory card.
For flashing I used the Tool Win32DiskImager (https://sourceforge.net/projects/win32diskimager/) to write it to the memory card. After that I connected the raspberry by lan to the router and it got an automatic IP-Adress

The standard login credentials are (connecting over SSH, by Putty):
```
username: root
password: raspberry
```

The first problem what we had was to identify each raspberry. So we decided to set a static IP-Address. We used the following commands for that

To install some helper programs: `apt-get get install nano`

Configuring Interface

```nano etc/networks/interfaces```
```
iface eth0 inet static
address 192.168.3.19
netmask 255.255.255.0
gateway 192.168.3.1
```

## 3. Seting up ssh
I followed the tutorial of https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2

For that I downloaded PuttyGen (http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)

First I created the right file
```
cd ~
mkdir .ssh
cd .ssh
nano authorized_keys
```
Then I set the permissions
```
chmod 700 ~/.ssh/ 
chmod 600 ~/.ssh/authorized_keys
```
Check permissions
```
ls -l 
```

## 4. Control the Raspberry with LEDs

For that I used wiringpi (http://wiringpi.com/download-and-install/). This is a library to easliy control the pins.

For resizing the space of the raspberry:`apt-get install raspi-config`
Then I entered it by:
```
raspi-config
```
and select the first option.

During configuring Ms. Norbisrath realized that the connection from the rapsberry to the breadboard was wrong so the connection did not work. The following picture is documenting the right setting:

![Image of raspberry with the right breadboard setting available at http://madner.eu/mcm/pics/01_02_BreadBoard.jpg](http://madner.eu/mcm/pics/01_02_BreadBoard.jpg "BreadBoard")

**Hint:**
*Red line must be up (south)*

To directly talk with the PI you need the following commands:
to get all pins with its wPis
```
gpio readall
```

Now we are using PIN 0 (what is mapped to PIN 16 on the board)
```
gpio mode 0 out
gpio write 0 1
```

## 5. Seeting up E-Mail notifier

I followed the instructions on:
https://learn.adafruit.com/raspberry-pi-e-mail-notifier-using-leds/prepare-python

While installing I got an error so I used the following command to avoid errors:
```
apt-get install python-dev
```

Since RPi.GPIO was not found I still needed to install RPi.GPIO by the following command
```
pip install RPi.GPIO
```
We finished the lecture with having problems installing the E-Mail Service. The following error occured:
> Problem with SSL.Context