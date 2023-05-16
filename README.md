# OSPCIAN
An Arch Linux Based PCI-DSS compliant OS
Verify the boot mode:
	ls /sys/firmware/efi/efivars

Verify the internet connection 
	ping archlinux.org

Enable NTP:
	timedatectl set-ntp true

Partition and format the drive:
	lsblk
	cfdisk /dev/sda
	
	mkfs.ext4 /dev/sda2

Mount the partitions:
	mount /dev/sda2 /mnt
	

Create a swap file:
	Fallocate -l 2G /mnt/swapfile)
	chmod 600 /mnt/swapfile
	mkswap /mnt/swapfile
	swapon /mnt/swapfile

Install the base system:
	pacstrap /mnt base linux linux-firmware nano networkmanager grub 

Generate an fstab file:
	genfstab -U /mnt >> /mnt/etc/fstab

Chroot into the new Arch Linux system:
	arch-chroot /mnt

Set the time zone:
	ln -sf /usr/share/zoneinfo/Asia/Calcutta /etc/localtime)
	hwclock --systohc

Generate locales:
	nano /etc/locale.gen
	locale-gen
	cho LANG=en_CA.UTF-8 >> /etc/locale.conf
	

Set hostname:
	echo archlinux >> /etc/hostname

Set root password:
	passwd


Install GRUB:
	grub-install /dev/sda
	nano /etc/default/grub
		
	grub-mkconfig -o /boot/grub/grub.cfg

Install KDE Plasma and KDE applications:
	pacman -S plasma-meta kde-applications

Enable SDDM and NetworkManager on boot:
	systemctl enable sddm NetworkManager

Unmount:
Unmount /mnt/boot
Unmount /mnt

Exit chroot environment and reboot into the new Arch Linux system:
	exit
	reboot
