Mac OS EFI partition mount
```
sudo diskutil list

sudo mkdir /Volumes/efi

sudo mount -t msdos /dev/disk0s1 /Volumes/efi

sudo diskutil umount /dev/disk0s1
```
