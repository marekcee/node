Own Public Config
```
[public]

path = /home/pi/.public
browseable = yes
writable = yes
read only = no
guest ok = yes
create mask = 0644
directory mask = 0755
force user = pi


[global]

public = yes
writable = yes
guest account = pi
```

Samba Config Example

Anonymous Share
```
sudo mkdir /srv/samba

sudo chmod a+rwx /srv/samba
```

Edit the /etc/samba/smb.conf file:
```
sudo nano /etc/samba/smb.conf

[global]
  workgroup = WORKGROUP
  server string = Samba Server

[anonymous]
  path = /srv/samba
  browseable = yes
  writable = yes
  read only = no

sudo systemctl restart smbd
```

Password-Protected Share
```
sudo addgroup smbgrp

sudo useradd shares -G smbgrp

sudo smbpasswd -a shares

sudo mkdir -p /srv/samba-secured

sudo chmod -R 0770 /srv/samba-secured
sudo chown root:smbgrp /srv/samba-secured
```
```
sudo nano /etc/samba/smb.conf

[global]
  workgroup = WORKGROUP
  server string = Samba Server

[secured]
  path = /srv/samba-secured
  valid users = @smbgrp
  browseable = yes
  writable = yes
  read only = no

sudo systemctl restart smbd
```

Additional Configuration Options
```
Set the log file location:log file = /var/log/samba-log.%m
Set the maximum log file size: max log size = 50
Specify the Kerberos or Active Directory realm: realm = MY_REALM
Include additional configuration files: include = /usr/local/samba/lib/smb.conf.%m
Configure Samba to use multiple interfaces: interfaces = eth0 192.168.97.199/255.255.252.0
Testing Changes
Run testparm to verify the configuration file for errors.
Restart Samba after making changes to the configuration file.
Remember to customize the configuration options according to your specific environment and requirements. This example provides a basic outline for setting up anonymous and password-protected shares with Samba.
```
