### Emojis

- Install:

```bash
pacman -S ttf-joypixels 
```

- Test it using [this site](https://unicode.org/emoji/charts/full-emoji-list.html).
- Make sure `ttf-dejavu` is not installed. It will conflict with real emojis.

### Font Config

- Create the following file on `~/.config/fontconfig/conf.d/01-emoji.conf`.
- After that, run `fc-cache -f; sudo fc-cache -f`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- Add emoji generic family -->
  <match target="pattern">
    <test qual="any" name="family"><string>emoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <!-- Aliases for the other emoji fonts -->
  <match target="pattern">
    <test qual="any" name="family"><string>Apple Color Emoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Segoe UI Emoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Segoe UI Symbol</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>EmojiOne</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Emoji One</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Android Emoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>NotoColorEmoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Noto Emoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Twemoji</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>EmojiSymbols</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <match target="pattern">
    <test qual="any" name="family"><string>Symbola</string></test>
    <edit name="family" mode="assign" binding="same"><string>JoyPixels</string></edit>
  </match>

  <!-- Do not allow any app to fallback to Symbola, ever -->
  <selectfont>
    <rejectfont>
      <pattern>
        <patelt name="family">
          <string>Symbola</string>
        </patelt>
      </pattern>
    </rejectfont>
  </selectfont>
</fontconfig>
```
