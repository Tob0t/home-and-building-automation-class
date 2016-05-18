## 0. Info
- Protocol: Session 03_Task1
- Date: 18.05.2016
- Time: 14:40 - 18:00
- Topic: Setup Programs

## 1. Setup PlatformIO
In order to use PlatformIO you need to install the debianpackage with the following commands:

    apt-get -f install
    dpkg packageio.deb

To be able to deploy over serial port you need to add yourself to the dialout group with the following command

    useradd -G dialout username

Or you can just edit the `/etc/group` file (look for `dialout:x:20:<your_username>`). Dont forget to log out and in again afterwards! You can check if you where successfull with the `groups` command.

## 2. Setup Arduino IDE

To get arudino you just need to download it from the web and move the extracted file in the `/opt`folder.
In this folder add execute rights to the install shell script and run it:

    chmod +x install.sh
    ./install.sh

## Install the PubSubClient
* Arduino IDE: Sketch -> Include Library -> Manage Libraries -> search and install PubSubClient