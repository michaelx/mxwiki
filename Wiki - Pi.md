# Basics

- SSH: ssh pi@<IP>
- Safe shutdown: `sudo shutdown -h now`
- Safe reboot: `sudo shutdown -r now`
- Get free space: `df -h`
- Get CPU processes: `top`
- Get CPU/GPU temperature: `vcgencmd measure_temp`
- Get CPU details: `cat /proc/cpuinfo`
- Get RAM details: `cat /proc/meminfo`

## Updating and upgrading

1. Update the system package list: `sudo apt-get update`
2. Upgrade all installed packages: `sudo apt-get dist-upgrade`

## Backup and restore SD card

**Backup**

1. Use Mac SD card reader. Cloning while running RaspPi is not the best idea.
2. Get list of disks and volumes: `diskutil list`
3. Create image and compress on the fly:

```sh
sudo dd if=/dev/rdisk1 bs=1m | gzip > ~/<destination>/pi.gz
```

> `if` = `input file`; prefix disk with `r` to point to the card’s raw storage space to speed up the process; `bs` = `block size`, 1MB (1m) is preferred by dd.

Use `ctrl + t` to view progress.

**Restore**

1. Use Mac SD card reader.
2. Unmount, but not eject, SD card to be able to write to it: `diskutil unmountDisk /dev/disk1`
3. Flash SD card: `gzip -dc ~/<source>/pi.gz | sudo dd of=/dev/rdisk1 bs=1m`