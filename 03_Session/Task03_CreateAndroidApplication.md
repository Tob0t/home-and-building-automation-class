## 0. Info
- Protocol: Session 03_Task3
- Date: 13.05.2016
- Time: 09:00 - 12:00
- Topic: Create Android Application for Lock

## 1. Setup
In our team I was assigned to create an android application to unlock a lock by NFC and over mqtt messages. For that I needed to integrate the paho-mqtt library what can be found at <https://github.com/eclipse/paho.mqtt.java>.
### NFC - Setup
To start the app when a NFC-Sticker is scanned the following intent filter need to be set in the AndroidManifest.xml:
```
 <intent-filter>
    <action android:name="android.nfc.action.TAG_DISCOVERED"/>
</intent-filter>
```
After reading a tag we read the *TAG-ID* with the following command:
```
intent.getParcelableExtra(NfcAdapter.EXTRA_TAG).getId();
```
## 2. Features
We implemented two functions in our application
### Verify Key
We decided to use commom NFC-Sticker which can be used as keys. To have a good flexibility we choose to use the unique **TAG-ID** as key. That key is send to the raspberry where it calculates a md5-hash of the **TAG-ID**. If the md5-hash is in a list of allowed md5 hashes than the lock will be opened for 10 seconds.
![Image Verify Key <http://madner.eu/mcm/pics/03_03_VerifyKey.png>](http://madner.eu/mcm/pics/03_03_VerifyKey.png "Verify Key")

### Add Key
We also integrated an easy option to add new keys. For that we are sending the unique **TAG-ID** with a field called **validUntil** to the raspberry which is adding that keys to its database.
![Image Verify Key <http://madner.eu/mcm/pics/03_03_AddKey.png>](http://madner.eu/mcm/pics/03_03_AddKey.png "Add Key")

## 3. Security
Since the standard settings for the broker of the mqtt protocl is public for everyone we need to change the settings. The easisest mehtod is to use a username and password authentificationg
## Username & password
The android application is authenticating with the following commands:
```
MqttConnectOptions connOpts = new MqttConnectOptions();
connOpts.setUserName(username);
connOpts.setPassword(password.toCharArray());
```

## Certificates
Since the certificates need to be set manually in the settings of each device and makes much effort we decided to skip it and prefer the username & password authentication. However we strongly recommend for production purpose that this option should be taken into account.