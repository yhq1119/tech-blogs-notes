# Setup your PI

### Download imager and write system into SD card
- Download the imager from raspberrypi.org
Credit: https://www.raspberrypi.org/downloads/
- Unplug the SD card from the Raspberry Pi
- Plug SD card to computer
- Write Raspberry OS image using Imager
  (Example: OS: Raspbian, SD: target SD card, write)
- After finished, plug SD card to raspberry pi
 
Notice: 
* The default user is ```pi```
* The default password is ```raspberry```

### connect the Raspberry Pi to computer
- Connect the raspberry pi to computer using USB-netcable
- ssh to your raspberry

```unix
ssh pi@raspberrypi.local
```
- configure the wifi connection
Credit: https://docs.dataplicity.com/docs/get-pi-connected-to-the-internet#

```linux
sudo nano /etc/network/interfaces
```
paste the following content into it
```vim
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man ahcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d

auto lo
iface lo inet loopback

iface eth0 inet manual

allow-hotplug wlan0
iface wlan0 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf

allow-hotplug wlan1
iface wlan1 inet manual
```

Configure the ```/etc/wpa_supplicant/wpa_supplicant.conf```
as following
```vim
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=AU

network={
    ssid="YOUR WIFI SSID"
    psk="PASSWORD OF YOUR WIFI"
    priority=5
}

```
After finished, try

```linux
sudo reboot
```
Then you can unplug it from your computer
After a short while you can connect to raspberry pi
```linux
ssh pi@raspberrypi.local
```
You can try if the Internet works using commands below
```bash
sudo ping -c 5 www.google.com
```
If you can receive the responses, it means successful setup.
Then you can use your raspberry pi without net cable connected to your computer.
