### Fix C cedilla

If not possible to use `ç` with `US` international layout, do the following:

- As `sudo`, go to `/usr/share/X11/locale/en_US.UTF-8`
- Edit the `Compose` file replacing 'Ć' by 'ç' and 'ć' by 'ç/'
- Save the file.

The following code, may be helpful:

```bash
cd /usr/share/X11/locale/en_US.UTF-8
cp Compose Compose.original
cat Compose.original | sed -e 's/Ć/ć/' -e 's/Ç/ç/' > Compose
```

### Fix on GTK

Do the following:

- Go to `/usr/lib/gtk-Y/X/immodule-files.d/`, where `X` and `Y` are the GTK version (`2.0` or `3.0`).

```
/usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules.cache
/usr/lib/x86_64-linux-gnu/gtk-2.0/2.10.0/immodules.cache
```

- On both, find the lines starting with "cedilla" "Cedilla" and add `:en` to the line. Something like this:

```
"cedilla" "Cedilla" "gtk30" "/usr/share/locale" "az:ca:co:fr:gv:oc:pt:sq:tr:wa:en"
```

### Instruct the system to load the cedilla 

Add those lines to /etc/environment:

```
GTK_IM_MODULE=cedilla
QT_IM_MODULE=cedilla
```



- References: https://superuser.com/a/1235405
