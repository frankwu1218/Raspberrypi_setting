To solve the issue of WAP WIFI encryption for remotely controll of raspberrypi.  

Get hash from the host laptop(password is the password for the specific WIFI)
```
echo -n [password] | iconv -t UTF-16LE | openssl md4
```
You will get a code. 

Use nano to edit the file "wpa_supplicant.conf" to change the ssid, identity and password id needed. The password here is the code you got from 
```
echo -n [password] | iconv -t UTF-16LE | openssl md4
```


For Raspberry Pi OS:
Upload "interfaces" and "wpa_supplicant.conf" to the boot file of Raspberrypi.  

For Raspberry Pi OS Lite:
Upload "interfaces" and "wpa_supplicant.conf" to the boot file of Raspberrypi.  
Log in: pi/raspberry
```
sudo -s
cd /etc/wpa_supplicant/
sudo raspi-config
```
trun on SSH and set other stuff up if needed.
