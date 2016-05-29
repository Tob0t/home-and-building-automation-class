## 0. Info
- Protocol: Session 06_Task3
- Date: 24.05.2016
- Time: 12:45 - 15:30
- Topic: Setup Philips Hue

## 1. Setup App
First we need to connect the Hue to the local network. Then we plug in the light bulbs. Following the FAQ at <https://www.dmlights.com/philips-hue-faq.l> and installing the android application from the playstore at <https://play.google.com/store/apps/details?id=com.philips.lighting.hue>. With that application we can control the light bulbs.

## 2. Connecting Hue to openHub
I followed the tutorial at <http://www.makeuseof.com/tag/getting-started-openhab-home-automation-raspberry-pi/>.

First you need to copy the right binding into your `addon` folder:

    org.openhab.binding.hue-1.8.2.jar 
    
After that you need to make some changes in the **openhab.cfg** file. Search for *hue* and configure it with the right ip address:

    # IP of the Hue bridge
    hue:ip=192.168.3.19
    hue:secret=makeuseofdotcom
    hue:refresh=10000
    
**Hint**: To get the right ip address just open <https://www.meethue.com/api/nupnp>.

After that you can save and exit the configuration file. Then you need to approve OpenHAB on the Hue Bridge by pressing the button on the front – you only need to do this once.

## 3. Troubleshooting
Then it should be able to control hue by OpenHAB. There I got the problem that it could not authorize. After upgrading to `org.openhab.binding.hue.v.1.8.3` I still got the same problem. By the help of one colleague we discovered a *Getting started* page of philips for debugging (<http://www.developers.meethue.com/documentation/getting-started>).

Following that example I found out that you need to add an already authorized username to the config file:

    hue:ip=<YOUR_IP_OF_THE_BRIDGE>
    hue:secret=B1zYcqgllbtc9yN2W6Gdk3m7ep7eSG1fEJ7kYvmc
    hue:refresh=10000

The line ```hue:secret=B1zYcqgllbtc9yN2W6Gdk3m7ep7eSG1fEJ7kYvmc``` should be filled with the secret of an already authorized username. Now openhub is connected to the Hue.

With a basic setup we can control the lights: 

```items/home.items```
    
    Switch LightBulb1 "Light Bulb 1" <hue> (Office) {hue="10"}
    Color LightBulb2 "Color Bulb 2" <hue> (Office) {hue="11"}

```sitemaps/home.sitemap```
    
    Frame label="Light Bulbs"{
        Switch item=LightBulb1
        Colorpicker item=LightBulb2
    }


## Sources
<https://github.com/openhab/openhab/wiki/Hue-Binding>
<http://www.makeuseof.com/tag/getting-started-openhab-home-automation-raspberry-pi/>
<http://www.developers.meethue.com/documentation/getting-started>