NETWORK

SSH
```
ssh pi@192.168.1.X
ssh pi@raspberry.local
```

SSH Key Reset
```
ssh-keygen -R 192.168.1.X
rm -rf ~/.ssh/*
```
------------------------------------------

TOR
```
sudo apt install tor
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
sudo usermod -a -G debian-tor pi
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
sudo apt install gparted
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

INSTALL BITCOIN CORE

Best to use other machine to verify SHAsums and signatures, input link through SSH after.
```
wget https://bitcoincore.org/bin/bitcoin-core-27.2/bitcoin-27.2-aarch64-linux-gnu.tar.gz
tar xzf bitcoin-27.2-aarch64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-27.2/bin/*
```

------------------------------------------
