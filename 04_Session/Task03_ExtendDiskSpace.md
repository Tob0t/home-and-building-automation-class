## 0. Info
- Protocol: Session 03_Task2
- Date: 18.05.2016
- Time: 14:40 - 18:00
- Topic: Extend Diskspace of Ubuntu Client

## 1. Extend Diskspace
I followed the tutorial what can be found at <http://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/>

Since I had suddenly the problem to not beeing able to install something anymore I realized that there is no disk space available anymore. For that I need to extend the diskspace.

First you need to navigate to your installed oracle program

    cd “C:\Program Files\Oracle\VirtualBox”
    
After that you can modify the size of your hard disk by navigating to the path of it:

    VBoxManage modifyhd “C:\Users\Chris\VirtualBox VMs\Windows 7\Windows 7.vdi” --resize 81920
    
## 2. Enlarge the Virtual Machine’s Partition
After that you still need to enlarge the partition by downloading *GParted*. This can be found at <http://gparted.sourceforge.net/download.php>.