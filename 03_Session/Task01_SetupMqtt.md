## 0. Info
- Protocol: Session 03_Task1
- Date: 13.05.2016
- Time: 09:00 - 12:00
- Topic: Setup MQTT

## 1. Setup
We used the message broker *Mosquitto* to which is implementing the MQTT protocol. Refering to the website <http://mosquitto.org/>
>MQTT provides a lightweight method of carrying out messaging using a publish/subscribe model. This makes it suitable for "Internet of Things" messaging such as with low power sensors or mobile devices such as phones, embedded computers or microcontrollers like the Arduino.
To install it on our raspberry I used the following commands:
```
apt-get install mosquitto
apt-get install mosquitto-clients
```

## 2. Publish & Subscribe
The following parameters are essential to know:
```
-m message
-t target
-h host
```

Now we can easily publis & subscribe with the following commands:
### Subscribe
```
mosquitto_sub -h localhost -t mqtt_test
```

### Publish
```
mosquitto_pub -h localhost -t mqtt_test -m "Hello mqtt"
```
## 3. Security
To ensure that only registered clients are allowed to publish/subscribe we need to set up some security. The easiest method is by doing it with a certificate.

The following commands need to be used:
```
/listen
/authenticate
```

See the manual page for more mosquitto security settings.

## 4. Python
To use mqtt with python there is an easy to use library called **PAHO**. It can be found at <http://www.eclipse.org/paho/>

**Hint**
If you are running the subscribing task and you want to stop it use the following command:
```
pkill -9 python
```