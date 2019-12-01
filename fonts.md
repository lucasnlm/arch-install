### Fonts

Install:

```bash
pacman -S ttf-liberation font-bh-ttf ttf-bitstream-vera ttf-croscore ttf-roboto noto-fonts ttf-cascadia-code ttf-fira-code
yay -S ttf-ms-win10 
```

### Emojis

- Install:

```bash
pacman -S ttf-joypixels 
```

- Test it using [this site](https://unicode.org/emoji/charts/full-emoji-list.html).
- Make sure `ttf-dejavu` is not installed. It will conflict with real emojis.

### Update cache

- After isntall all fonts, run:

```bash
fc-cache
```
