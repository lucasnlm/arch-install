# Arch Linux Install

## Before start:

Get the Arch Linux ISO and write it to an USB stick using [`dd`](https://pt.wikipedia.org/wiki/Dd_(Unix)), [`Rufus`](https://rufus.ie/), [`UNetbootin`](https://unetbootin.github.io/), or [`balenaEtcher`](https://www.balena.io/etcher/).

You can get the ISO [here](https://www.archlinux.org/download/).

## Boot

Boot to the Arch live system image.

## Keyboard

Make sure you are using the right keyboard layout. By default, Arch uses `US` layout. But, you can change it using the following command:

```bash
# Full layout list: 
# ls /usr/share/kbd/keymaps/**/*.map.gz

loadkeys br-abnt2
```

## Internet

Make sure you have an active internet connection. To Wifi connections, use `wifi-menu`.

```bash
ping archlinux.org
```

## UEFI

Verify if you are using na UEFI or BIOS motherboard. To do it, run the following command:

```bash
ls /sys/firmware/efi/efivars
```

If the directory does not exist, the system may be booted in BIOS or CSM mode. Refer to your motherboard's manual for details.

## Update the system clock

Use `timedatectl` command to ensure the system clock is accurate. Run the following command:

```bash
timedatectl set-ntp true
```

## Partitioning without Cryptography

Run the following commands:

```bash
fdisk -l
cfdisk /dev/nvme0n1
```

If your hardware supports UEFI, select `gpt`. Otherwise select `dos`.

Create the following partitions:

| Partition | Location       | Size | Type             |
| --------- | -------------- | ---- | ---------------- |
| Boot      | /dev/nvme0n1p1 | 256M | EFI System       |
| /         | /dev/nvme0n1p2 | 50G  | Linux Filesystem |
| /home     | /dev/nvme0n1p3 | \*   | Linux Filesystem |
| Swap     | /dev/nvme0n1p4 | 24GB   | Swap

Check if the partitions were created:

```bash
fdisk -l /dev/nvme0n1
```

If your storage device is SATA, it will be `sda` instead of `nvme0n1`.

## Formatting and making the filesystems

Run the following commands to format the partitions:

```bash
mkfs.vfat -F32 -n EFI /dev/nvme0n1p1
mkfs.ext4 /dev/nvme0n1p2
mkfs.ext4 /dev/nvme0n1p3
```

For swap:

```bash
mkswap /dev/nvme0n1p4
swapon /dev/nvme0n1p4
```

And then mount them:

```bash
mount /dev/nvme0n1p2 /mnt
mkdir -p /mnt/boot/EFI
mount /dev/nvme0n1p1 /mnt/boot
mkdir /mnt/home
mount /dev/nvme0n1p3 /mnt/home
ls /mnt
```

Check if they are correctly mounted using:

```bash
findmnt
```

## Base install

Run the following commands to install the base:

```bash
pacstrap /mnt base base-devel linux-zen linux-zen-headers
```

## Create fstab

Run the following command to generate the `fstab` file.

```bash
genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

Make sure your `fstab` file has all previously created partitions.

## Create the swap file

This is optional. Only do it if you didn't created Swap as partition.

Run the following:

```bash
fallocate -l 8G /mnt/swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

Then, add the following to `fstab` file:

```bash
# Swap
/swapfile none swap defaults 0 0
```

Check if swap is working running `free -h`.

## Check Swappiness

Edit the file `/etc/sysctl.conf` and set the swappiness value.

```bash
sudo nano /etc/sysctl.conf

# Add
vm.swappiness=10
vm.vfs_cache_pressure=50
```

## Go to the new system

```bash
arch-chroot /mnt

mkinitcpio -p linux-zen
uname -r
```

## Enabling Trim to SSD devices

Run the following:

```bash
sed -i 's/relatime/noatime/' /mnt/etc/fstab
arch-chroot /mnt systemctl enable fstrim.timer
```

## Sync time

Run the following command:

```bash
ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/timezone
hwclock --systohc --utc
```

## Locale

Uncomment `en_US.UTF-8` in `/etc/locale.gen`, then run:

```bash
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
echo KEYMAP=us-acentos > /etc/vconsole.conf
```

## Install rEFInd

Run the following commands to install rEFInd

```bash
pacman -S refind-efi
refind-install
```

Edit `/boot/refind_linux.conf`

```
"Boot with standard options"  "root=/dev/nvme0n1p2 rw initrd=/boot/initramfs-linux-zen.img initrd=/boot/initramfs-linux-zen-fallback.img quiet splash"
```

## Install yay

``` bash
pacman -S git
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

## Configure pacman

Edit `/etc/pacman.conf` and uncomment `Color` and `multilib`.

