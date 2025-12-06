# network
- iwctl
- station wlan0 scan
- station wlan0 get-networks
- station wlan0 connect name
- exit
- ping google.com

# time
- timedatectl set-ntp true
- timedatectl status

# disk
To list the physical drives and it's partitions
- lsblk
- fdisk -l

### partition 
We need these partitions,
550M -> EFI partition (uefi) (fat32)
Rest -> root partition 

- sudo fdisk /dev/nvme0n1
EFI:
- n
- last partition: +550M
- t
- uefi

Root:
- n

- w
Write those changes 
### format
EFI:
- mkfs.fat -F32 /dev/nvme0n1p4
Root:
- mkfs.ext4 /dev/nvme0n1p5

# system files installation 
- mount /dev/nvme0n1p5 /mnt
- pacstrap /mnt base linux linux-firmware

## Generate file system table
- genfstab -U /mnt >> /mnt/etc/fstab

# chroot into mnt
- arch-chroot /mnt
- pacman -S vim sudo iwd 
- ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime
- hwclock -w
- vim /etc/locale.gen
- nano /etc/locale.gen
	Uncomment `#en_US.UTF-8 UTF-8`
- locale-gen
- vim /etc/hostname 
- vim /etc/hosts
```sh
127.0.0.1 localhost
::1       localhost
127.0.1.1 hostname.localdomain hostname
```
# Root and users
- passwd
- useradd -m name
- passwd name
- usermod -aG wheel,audio,video,optical,storage name
- EDITOR=nano visudo
	Uncomment the line `#%wheel ALL=(ALL) ALL`
# Boot manager
- pacman -S refind
- mount linux_efi /boot
- refind-install
- efibootmgr (check)

1) Edit refind.conf with /dev/nvme0n1p4 (boot)
2) edit refind_linux.conf with/dev/nvme0n1p5 (root) and delete first two lines

- pacman -S linux-headers
Should have kernal files at /boot (mounted linux EFI partition)
# in the main system after reboot
- nmcli device wifi list
- nmcli device wifi connect ssid password psw

# gnome
- sudo pacman -S gnome gnome-extras gnome-tweaks gnome-extensions
- systemctl enable gdm
- systemctl start gdm

# yay
- sudo pacman -S --needed base-devel git
- git clone https://aur.archlinux.org/yay-git.git
- cd yay
- makepkg -si