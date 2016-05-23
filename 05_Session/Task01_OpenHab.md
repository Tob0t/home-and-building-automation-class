## 0. Info
- Protocol: Session 05_Task1
- Date: 18.05.2016
- Time: 08:50 - 12:05
- Topic: Working with OpenHAB

## 1. Running 2 LEDs blinking
I followed the tutorial what can be found at <https://mcuoneclipse.com/2015/12/24/blinky-led-with-openhab-on-raspberry-pi/>

### Items file
First you need to define the items. For that you need to create a file in the following folder: ``` /opt/openhab/configurations/items/home.items``` and define the gpio ports for the leds

    Switch RaspiLED1(Central){ gpio="pin:18" }
    Switch RaspiLED2(Central){ gpio="pin:23" }
    Group:Switch Central
    
This tells that I’m using a ‘switch’ (on/off) item named *RaspiLED1* and *RaspiLED2*  which is using the GPIO binding on pin 18 and pin 23. Another Switch is added which is named *Central* at can be on or off.
A detailed explanation of all the items can be found at <https://github.com/openhab/openhab/wiki/Explanation-of-items>.

### Sitemap file
Then you need to define the sitemap. For that you need to create a file in the following folder: ``` /opt/openhab/configurations/sitemaps/home.sitemapss``` and define the structure of the sitemap.
        
    sitemap home label="Home"{
        Frame label="Rasperry Pi GPIO"{
            Switch item=RaspiLED1
            Switch item=RaspiLED2
        }
        Frame label="Central Switch"{
            Switch item=Central
        }
    }
    
This is basically defining the structure and the appearance of the controls. 

## 2. Using hardware button
In the second exercise there needs to be a hardware button used to control the lights.
For that you need to make the right setup what is best described in the following picture:
![Image of raspberry with the right setting for a switch at <http://madner.eu/mcm/pics/05_01_SetupButton.jpg.jpg>](http://madner.eu/mcm/pics/05_01_SetupButton.jpg.jpg "Setup Button")

Then you need to define an input device with the following command

    Contact MyButton {gpio="pin:25 activelow:yes force:yes"}

ActiveLow defines that the CLOSED state is ON when the button is pressed.
Furthermore we need to add a rule that triggers the LED change:
    
    rule "toggle LED 1 when HWButton pressed"
    when
        Item MyButton changed
    then
        RaspiLED1.sendCommand(if(RaspiLED1.state!=OFF) OFF else ON)
    end

After the first try the trigger did not work. Following the bugreport of <https://community.openhab.org/t/raspian-jessie-gpio-input/3448/27> and installing 2 new gpio jars I got the trigger result.

## 3. Setting up Timer
For setting up we need to define first a new item:
    
    Switch LedTimer "LED Timer" {gpio="pin:12 force:yes"}
    
Then we need to add a switch to the sitemap to activate the LED:    
    
    Switch item="LedTimer"
    
Then we define the following rule:
    
    var Timer timer
    rule "Turn off TimeLED"
    when
        Item LedTimer changed to ON
    then
        timer = createTimer(now.plusSeconds(5))[|
          LedTimer.sendCommand(OFF)
          timer=null;
        ]
    end 

**Hint*: To use that example you need to import `org.openhab.model.script.actions.Timer`

This rule is listening to the event that the LED is turned on and than creates a timer which is turning off the led after 5 seconds.





