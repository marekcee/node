RUN BITCOIN
```
bitcoind -daemon

/usr/local/bin/bitcoin-qt
```
STOP
```
bitcoin-cli stop
```
AUTOSTART
```
crontab -e
@reboot /usr/local/bin/bitcoind -daemon
```
CONFIG
```
sudo nano /home/pi/.bitcoin/bitcoin.conf
```
------------------------------------------

CLI INTERACTIONS
```
bitcoin-cli -getinfo
bitcoin-cli -netinfo
bitcoin-cli getblockchaininfo
bitcoin-cli getblockcount
bitcoin-cli getnetworkinfo
bitcoin-cli getconnectioncount
```
------------------------------------------

NETWORK
```
ssh pi@192.168.1.X
ssh pi@raspberry.local
```

Mac Key Reset
```
ssh-keygen -R 192.168.1.X
rm -rf ~/.ssh/*
```
```
nmtui
ifconfig
iwlist rate
nmcli
```
------------------------------------------

RASPBERRY COMMANDS
```
sudo raspi-config
vcgencmd measure_temp
sudo apt-get update && sudo apt-get upgrade
```
```
top
htop
free -h
```
```
sudo reboot
sudo shutdown -h now
exit
```
------------------------------------------

TOR
```
sudo apt-get install tor
sudo nano /etc/tor/torrc
```

add:
```
ControlPort 9051
CookieAuthentication 1
CookieAuthFileGroupReadable 1
```

add to bitcoin.conf:
```
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1
```
```
sudo systemctl enable tor
sudo systemctl start tor
sudo systemctl start/stop tor
```
```
ps -eo user,group,comm |egrep 'bitcoind|bitcoin-qt' |awk '{print "Bitcoin user: " $1}'
usermod -a -G tor BITCOIN_USER
```
#Group should be 'debian-tor'

------------------------------------------

NORD VPN
```
sh <(curl -sSf https://downloads.nordcdn.com/apps/linux/install.sh)
```
```
nordvpn login (desktop and browser maybe necessary)
nordvpn whitelist add subnet 192.168.1.0/24
nordvpn c p2p / sk / sk59
nordvpn d
```
------------------------------------------

HARD DRIVE

CLI
fdisk
mkfs

GUI
sudo apt-get install gparted

sudo blkid
copy UUID
sudo umount /dev/sda1
sudo mkdir /home/pi/.bitcoin
sudo chown -R pi:pi /home/pi/.bitcoin
sudo mount /dev/sda1 /home/pi/.bitcoin
df -h

AUTOMOUNT

sudo nano /etc/fstab
PARTUUID=********-** /home/pi/.bitcoin ext4 defaults,auto,users,rw,nofail 0 0

------------------------------------------

INSTALL BITCOIN CORE FROM DEV

#Best to use other machine to verify SHAsums and signatures, input link after.

wget https://bitcoincore.org/bin/bitcoin-core-26.1/bitcoin-26.1-aarch64-linux-gnu.tar.gz
tar xzf bitcoin-26.1-aarch64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-26.1/bin/*

non-standard dir: -datadir=/mnt/btc

------------------------------------------
