Samba Config Example
Based on the provided search results, here is a comprehensive Samba configuration example:

Anonymous Share
Create a directory for sharing: sudo mkdir /srv/samba
Set permissions to allow anonymous access: sudo chmod a+rwx /srv/samba
Edit the /etc/samba/smb.conf file:
[global]
  workgroup = WORKGROUP
  server string = Samba Server

[anonymous]
  path = /srv/samba
  browseable = yes
  writable = yes
  read only = no

Restart Samba: sudo systemctl restart smbd
Password-Protected Share
Create a new group: sudo addgroup smbgrp
Create a new user: sudo useradd shares -G smbgrp
Set a password for the user: sudo smbpasswd -a shares
Create a directory for the password-protected share: sudo mkdir -p /srv/samba-secured
Set permissions: sudo chmod -R 0770 /srv/samba-secured and sudo chown root:smbgrp /srv/samba-secured
Edit the /etc/samba/smb.conf file:
[global]
  workgroup = WORKGROUP
  server string = Samba Server

[secured]
  path = /srv/samba-secured
  valid users = @smbgrp
  browseable = yes
  writable = yes
  read only = no

Restart Samba: sudo systemctl restart smbd
Additional Configuration Options
Set the log file location: log file = /var/log/samba-log.%m
Set the maximum log file size: max log size = 50
Specify the Kerberos or Active Directory realm: realm = MY_REALM
Include additional configuration files: include = /usr/local/samba/lib/smb.conf.%m
Configure Samba to use multiple interfaces: interfaces = eth0 192.168.97.199/255.255.252.0
Testing Changes
Run testparm to verify the configuration file for errors.
Restart Samba after making changes to the configuration file.
Remember to customize the configuration options according to your specific environment and requirements. This example provides a basic outline for setting up anonymous and password-protected shares with Samba.
