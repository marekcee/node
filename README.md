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

SSH
```
ssh pi@192.168.1.21
ssh pi@satoshi.local
```

SSH Key Reset
```
ssh-keygen -R 192.168.1.21
rm -rf ~/.ssh/*
```

NETWORK CONFIG
```
sudo nmtui
ifconfig
iwlist rate
nmcli
rfkill
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

MAC VNC
```
sudo systemctl enable vncserver-x11-serviced
sudo vncpasswd -service
sudo nano /etc/vnc/config.d/common.custom
add: Authentication=VncAuth
sudo systemctl restart vncserver-x11-serviced
```

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
onion=127.0.0.1:9050
listen=1
bind=127.0.0.1
```
```
sudo systemctl enable/disable tor
sudo systemctl start/stop/restart tor
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
```
fdisk
mkfs
```

GUI
```
sudo apt-get install gparted
```
```
sudo blkid
copy UUID
sudo umount /dev/sda1
sudo mkdir /home/pi/.bitcoin
sudo chown -R pi:pi /home/pi/.bitcoin
sudo mount /dev/sda1 /home/pi/.bitcoin
df -h
```

AUTOMOUNT
```
sudo nano /etc/fstab
PARTUUID=********-** /home/pi/.bitcoin ext4 defaults,auto,users,rw,nofail 0 0
```
------------------------------------------

INSTALL BITCOIN CORE FROM DEV

#Best to use other machine to verify SHAsums and signatures, input link after.
```
wget https://bitcoincore.org/bin/bitcoin-core-27.1/bitcoin-27.1-aarch64-linux-gnu.tar.gz
tar xzf bitcoin-27.1-aarch64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-27.1/bin/*
```
non-standard dir: -datadir=/mnt/btc

------------------------------------------

INSTALL BRAVE
```
sudo apt install curl

sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```

------------------------------------------

INSTALL PROTONVPN
```
wget https://repo.protonvpn.com/debian/dists/stable/main/binary-all/protonvpn-stable-release_1.0.3-3_all.deb
sudo dpkg -i ./protonvpn-stable-release_1.0.3-3_all.deb && sudo apt update
echo "de7ef83a663049b5244736d3eabaacec003eb294a4d6024a8fbe0394f22cc4e5  protonvpn-stable-release_1.0.3-3_all.deb" | sha256sum --check -
sudo apt install proton-vpn-gnome-desktop
sudo apt install libayatana-appindicator3-1 gir1.2-ayatanaappindicator3-0.1 gnome-shell-extension-appindicator
```
