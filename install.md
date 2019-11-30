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

### Go to the new system

```bash
arch-chroot /mnt
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
