## 0. Info
- Protocol: Session 02_Task1
- Date: 12.05.2016
- Time: 09:00 - 12:00
- Topic: Port Reflection Setup

## 1. Background
For getting background information it is easy to access the man-page from ssh under <http://www.openssh.com/manual.html>
The main information what I need is the following `-L`  means local tunnel `-R` means remote tunnel. A second good tutorial about Portforwarding can be found here: https://www.raspberrypi.org/documentation/remote-access/access-over-Internet/internetaccess.md

## 2. Portforwarding
For local portforwarding you can use the following command 
```
ssh <SERVER-IP> -p 22 -L <SOURCE-PORT>:<DESTINATION-IP>:<DESTINATION-PORT>
```

Now you can go to `<DESTINATION-IP>:<SOURCE-PORT>` which should forward you to `<DESTINATION-IP>:<DESTINATION-PORT>`

### Example
**Hint**: 
*Port 22 mapped to 4242*

```
ssh ulno.net -p 4242
ssh ulno-vps@ulno.net -p 4242 -L 10022:localhost:80
```
If you cannot access a specific website (f.e <http://www.heise.de>) but you can access the server than you can use the following command
```
ssh ulno-vps@ulno.net -p 4242 -L 10022:heise.de:80
```
Now you can go to `http://www.ulno.net:10022` which should forward you to `heise.de`.

### Port Forwarding on raspberry
With the same procedure you can make your raspberry public available by ssh (**Warning**: As stated in the raspberrypi documentation this method is a security risk since it is skipping any firewall).
> One disadvantage of port forwarding is that it exposes a network port on your private LAN to the public Internet. This is a known security vulnerability and must be managed carefully.

All you need to do is to change the parameter to `-R`.

For example: for a raspberry running on `192.168.0.19` and SSH on port `22`
```
ssh ulno-vps@ulno.net -p 4242 -R "*:10022:192.168.0.19:22"
```

However a secure alternative to port forwarding is to use the *Weaved service* as recommended at <https://www.raspberrypi.org/documentation/remote-access/access-over-Internet/internetaccess.md>. It creates a a private Internet VPN connection service to your raspberry.

