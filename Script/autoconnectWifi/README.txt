Switching between known Wifi networks

1. File /home/Pi/Desktop/DistCloud

country=GB  

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1


network={
	
ssid="DistCloud"
	
psk="qwer1234"

}


2. File /home/Pi/Desktop/icnslab

country=GB   

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1


network={
	
ssid="icnslab"
	
psk="iloveicns"

}

3. Then create a script for switching between networks, create file switchwifi by cmd: sudo nano switchwifi

#!/bin/bash


cp /home/pi/Desktop/$1 /etc/wpa_supplicant/wpa_supplicant.conf


ifdown wlan0

dhclient -r wlan0

ifup wlan0

dhclient -v wlan0


echo

iwconfig wlan0

ifconfig wlan0

4. Give permission to file switchwifi
sudo chmod +x switchwifi

Then run the connectWifi.py, before that remember to install module "wifi" by cmd: sudo pip install wifi
sudo python connectWifi.py


5. Notice: If there's error, check

-----Configuration of /etc/network/interfaces------

# interfaces(5) file used by ifup(8) and ifdown(8)


# Please note that this file is written to be used with dhcpcd

# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'


# Include files from /etc/network/interfaces.d:

source-directory /etc/network/interfaces.d


allow-hotplug wlan0

iface wlan0 inet manual

wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

------Configuration of /etc/wpa_supplicant/wpa_supplicant.conf----

ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev

update_config=1

country=GB


network={
	
ssid="icnslab"
	
psk="iloveicns"

}

