# Mounting nvme ssd

### Identify the drive
sudo fdisk -l

### Format
sudo mkfs.ext4 /dev/sdb1

### Temporarily mount
sudo mkdir /mnt/my_ssd
sudo mount /dev/sdb1 /mnt/my_ssd

### Mount permanently
blkid
sudo nano /etc/fstab
UUID=your-uuid-goes-here /mnt/my_ssd ext4 defaults 0 0

sudo mount -a