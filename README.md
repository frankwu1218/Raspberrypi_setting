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
```
sudo reboot
```


--------------------
#### We use the same as jetbot module for remotely control via jupyternotebook.(password is "jetbot")
#### Install jupyter lab
```
cd ~/
sudo apt install python3-smbus curl cmake -y
git clone https://github.com/lbaitemple/jetbot_nvidia_nano jetbot
cd ~/jetbot
sudo python3 setup.py install
sudo pip3 install packaging ipywidgets
chmod +x jupyter.sh
./jupyter.sh 
```

##### If not successfully run, please use the following commands
```
cd ~/jetbot/jetbot/utils
python3 create_stats_service.py
sudo mv jetbot_stats.service /etc/systemd/system/jetbot_stats.service
sudo systemctl enable jetbot_stats
sudo systemctl start jetbot_stats
python3 create_jupyter_service.py
sudo mv jetbot_jupyter.service /etc/systemd/system/jetbot_jupyter.service
sudo systemctl enable jetbot_jupyter
sudo systemctl start jetbot_jupyter
```
