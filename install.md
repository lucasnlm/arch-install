### Base install

Run the following commands to install the base:

```bash
pacstrap /mnt base base-devel linux-zen linux-zen-headers
```

### Create fstab

Run the following command to generate the `fstab` file.

```bash
genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

Make sure your `fstab` file has all previously created partitions.

### Create the swap file

This is optional. Run the following:

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

#### Check Swappiness

Edit the file `/etc/sysctl.conf` and set the swappiness value.

```bash
sudo nano /etc/sysctl.conf

# Add
vm.swappiness=10
vm.vfs_cache_pressure=50
```

### Go to the new system

```bash
arch-chroot /mnt

mkinitcpio -p linux-zen
uname -r
```

### Enabling Trim to SSD devices

Run the following:

```bash
sed -i 's/relatime/noatime/' /mnt/etc/fstab
arch-chroot /mnt systemctl enable fstrim.timer
```

### Sync time

Run the following command:

```bash
ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/timezone
hwclock --systohc --utc
```

### Locale

Uncomment `en_US.UTF-8` in `/etc/locale.gen`, then run:

```bash
locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
echo KEYMAP=us-acentos > /etc/vconsole.conf
```
