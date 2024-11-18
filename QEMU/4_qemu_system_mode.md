
## Creating SD Card
```sh
qemu-img create -f raw sd-card.img 32G
sudo parted sd-card.img mklabel msdos
sudo parted sd-card.img mkpart primary fat32 1MiB 256MiB
sudo parted sd-card.img mkpart primary ext4 256MiB 100%
```


# ARCH Linux
```sh
wget http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-aarch64-latest.tar.gz
mkdir archLinuxARM64
tar -xzf ArchLinuxARM-rpi-aarch64-latest.tar.gz -C ./archLinuxARM64
```
## Loop Device
```sh
# Create loop devices
sudo losetup -fP sd-card.img

# Check which loop device was created
losetup -a

sudo mkfs.vfat /dev/loop14p1
sudo mkfs.ext4 /dev/loop14p2
sudo parted sd-card.img print
```
## Mount Points
```sh
sudo mkdir /mnt/boot
sudo mkdir /mnt/rootfs

sudo mount /dev/loop14p1 /mnt/boot
sudo mount /dev/loop14p2 /mnt/rootfs


sudo rsync -a ./archLinuxARM64/boot/ /mnt/boot/
sudo rsync -a ./archLinuxARM64/ /mnt/rootfs/

# clean up
sudo umount /mnt/boot
sudo umount /mnt/rootfs
sudo losetup -d /dev/loop14
```


## Start QEMU
```sh
qemu-system-aarch64 \
	-M raspi3b \
	-m 1G \
	-smp 4 \
	-kernel ./archLinuxARM64/boot/kernel8.img \
	-dtb ./archLinuxARM64/boot/bcm2710-rpi-3-b.dtb \
	-drive file=./sd-card.img,format=raw,if=sd \
	-serial pty \
	-serial mon:stdio \
	-append "root=/dev/mmcblk0p2 rw console=ttyAMA0,115200 loglevel=7 earlyprintk"
```
