### My Arch Linux Install

#### Before start:

Get the Arch Linux ISO and write it to a USB stick using [`dd`](https://pt.wikipedia.org/wiki/Dd_(Unix)), [`Rufus`](https://rufus.ie/), [`UNetbootin`](https://unetbootin.github.io/) or [`balenaEtcher`](https://www.balena.io/etcher/).

You can get the ISO [here](https://www.archlinux.org/download/).

#### Boot

Boot to the Arch live system image.

#### Keyboard

Make sure you are using the right keyboard layout. By default, Arch uses `US` layout. But, you can change it using the following command:

```bash
# Full layout list: 
# ls /usr/share/kbd/keymaps/**/*.map.gz

loadkeys br-abnt2
```

### Internet

Make sure you have an active internet connection. To Wifi connections, use `wifi-menu`.

```bash
ping archlinux.org
```

### UEFI

Verify if you are using na UEFI or BIOS motherboard. To do it, run the following command:

```bash
ls /sys/firmware/efi/efivars
```

If the directory does not exist, the system may be booted in BIOS or CSM mode. Refer to your motherboard's manual for details.

### Update the system clock

Use `timedatectl` command to ensure the system clock is accurate. Run the following command:

```bash
timedatectl set-ntp true
```

