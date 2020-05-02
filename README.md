# raspberryPiSamba
Setting up Samba on your Raspberry Pi 

## Steps
1. Use balenaEtcher to flash the raspbian system  
2. Enable ssh 
touch /boot/ssh 
3. Use ethernet cable connect pi to PC
4. ping pi, get ip  
ping -4 raspberrypi 
5. ssh to pi  
pi  
raspberry 
6. Change pi configuration  
sudo raspi-config 
> change password, hostname, auto login to pi desktop, resolution, open vnc  

Error: pi cannot currently show the desktop 
> You forgot to set: auto login to pi desktop, change resolution  
7. vnc to pi hostname 
set timezone, language  
restart 
8. install raspap(optional)[https://github.com/billz/raspap-webgui]  
```
sudo apt-get update
sudo apt-get dist-upgrade
# if you use ssh to reboot, append sudo
sudo reboot
curl -sL https://install.raspap.com | bash
All yes

Use laptop to log in raspap
IP address: 10.3.141.1
Username: admin
Password: secret
DHCP range: 10.3.141.50 to 10.3.141.255
SSID: raspi-webgui
Password: ChangeMe

# change configuration
SSID: ChiTown2
Password: 
IP address: 192.168.4.1
DHCP range: 192.168.4.50 to 192.168.4.250

```
9. install samba[https://pimylifeup.com/raspberry-pi-samba/]  
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install samba samba-common-bin
mkdir /share
sudo nano /etc/samba/smb.conf

# add the following to the bottom. A little different from the tutorial
[share]
path = /share
writeable=Yes
create mask=0777
directory mask=0777
public=no

sudo smbpasswd -a pi
sudo systemctl restart smbd
hostname -I
```





