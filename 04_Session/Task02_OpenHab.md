## 0. Info
- Protocol: Session 03_Task2
- Date: 18.05.2016
- Time: 14:40 - 18:00
- Topic: Setup OpenHAB

## 1. Setup OpenHAB
I followed the tutorial what can be found at <http://www.openhab.org/getting-started>

For using openHab you need to have java installed with the following command:
    
    apt-get install oracle-java7-jdk
    
After that you can download the openHAB runtime. You may need to install `unzip`. After that you need to move the files to `/opt/openhab`. 
    
    wget https://bintray.com/artifact/download/openhab/bin/distribution-1.8.2-runtime.zip
    apt-get install unzip
    unzip distribution-1.8.2-runtime.zip -d /opt/openhab
    cd /opt/openhab/configurations
    cp openhab_default.cfg openhab.cfg
    cd ../

Then you can execute the starscript.
   
    cd ./start.sh

After that you can go to the website to check if openhab is running http://192.168.0.101:8080/openhab.app?sitemap=demo