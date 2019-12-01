### Install yay

``` bash
pacman -S git
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

### Configure pacman

Edit `/etc/pacman.conf` and uncomment `Color` and `multilib`.
