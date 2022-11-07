#### raspberry pi wifi personal 

copy ```/raspberry_pi_wifi_personal/wpa_supplicant.conf``` to boot file of raspberrypi.



#### raspberry pi wifi enterprise

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

####
copy ```/raspberry_pi_wifi_personal/wpa_supplicant.conf``` to /etc/wpa_supplicant and replace the original file "wpa_supplicant.conf"


```
sudo -s
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
git clone https://github.com/frankwu1218/jetbot_nvidia_nano-1 jetbot
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

#### oled info display(https://www.youtube.com/watch?v=lRTQ0NsXMuw)
```
sudo apt-get update
sudo apt-get full-upgrade -y
sudo reboot
sudo apt-get install python3-pip
sudo pip3 install --upgrade setuptools
sudo pip3 install --upgrade adafruit-python-shell
wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/raspi-blinka.py
sudo python3 raspi-blinka.py
sudo i2cdetect -y 1
sudo pip3 install adafruit-circuitpython-ssd1306
sudo apt-get install python3-pil
git clone https://github.com/mklements/OLED_Stats.git
cd OLED_Stats
python3 stats.py (display)
cp PixelOperator.ttf ~/PixelOperator.ttf
cp stats.py ~/stats.py
cp fontawesome-webfont.ttf ~/fontawesome-webfont.ttf
```
```
cd
crontab –e
```
type ```@reboot cd /home/pi/OLED_Stats && python3 stats.py &```

```sudo reboot```


#### NODE-RED setup. 
```
sudo apt update
sudo apt upgrade -y
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered) --node14
sudo systemctl enable nodered.service
```




