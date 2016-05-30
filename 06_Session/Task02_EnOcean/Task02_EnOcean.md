## 0. Info
- Protocol: Session 06_Task2
- Date: 24.05.2016
- Time: 12:45 - 15:30
- Topic: EnOcean Setup

## 1. Setup
First we need to connect the enOcean receiver to the raspberry.
![Image of raspberry connected to enOcean <http://madner.eu/mcm/pics/06_01_SetupEnOcean.jpg>](http://madner.eu/mcm/pics/06_01_SetupEnOcean.jpg "Setup EnOcean")

### Disable Serial Console

    #Spawn a getty on Raspberry Pi serial line
    #T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100
    
### Modify start script
Add the following line to ```start.sh``` and optionally ```start-debug.sh```:

    -Dgnu.io.rxtx.SerialPorts=/dev/ttyAMA0 \
    
### Modify configuration
Open ```openhab.cfg``` and look for *EnOcean Binding* and add the following line

    # EnOcean USB adapter serial port   
    enocean:serialPort=/dev/ttyAMA0
    
### Import library
Finall you just need to import the following jar in ```opt/openhab/addons``` and restart the raspberry:
    
    org.openhab.binding.enocean-1.8.2.jar
    
## 2. Light Up and Show temperature
The goal is to light up a LED when pressing a wireless connected enocean button via OpenHAB and to show the temperature of a enocean sensor on the openHAB website.

### Items
To achieve that you need to edit first the ```items/led.items``` file.

    Switch Enocean {enocean="{id=00:29:89:31, eep=F6:02:01}"}
    Number Temperature "Temperature [%.1f °C]" <temperature> {enocean="{id=01:81:B8:91, eep=A5:02:05, parameter=TEMPERATURE}"}
    
Following things need to be considered:

- ID: The device ID, printed on the device or found by debugging
- EEP: Enocean Equipment Protocol, what kind of protocol to use depending on the kind of device (<https://github.com/openhab/openhab/wiki/EnOcean-Binding>)

### Sitemaps
Furthermore the ```sitemaps/led.sitemap``` also needs to be changed:
    
    Frame label="Enocean"{
		Text item=Temperature valuecolor=[>25="orange",>15="green",>5="orange",<=5="blue"]
	}
	
This will display the temperature in a color that represents the temperature value.

### Rules
For triggering the button a rule needs to be defined in ```rules/led.rules```:

    rule switch_light_on_with_enocean
        when
        	Item Enocean received command ON
        then
        	if (LedYellow.state == OFF) sendCommand(LedYellow, ON)
        end
    
    rule switch_light_off_with_enocean
        when
                Item Enocean received command OFF
        then
                if (LedYellow.state == ON) sendCommand(LedYellow, OFF)
        end
		
		
		
## Sources
- <https://github.com/openhab/openhab/wiki/EnOcean-Binding>
- <https://www.element14.com/community/community/design-challenges/forget-me-not/blog/2014/08/10/ip-post-5-tutorial-for-interfacing-openhab-with-enocean-pi>