### Install Android Studio on Arch Linux

Run the following:

```bash
sudo pacman -Syy
yay -S android-studio android-sdk android-sdk-platform-tools android-sdk-build-tools 

groupadd users
gpasswd -a $USER users
sudo chown -R root:users /opt/android-studio
sudo chmod -R g+w /opt/android-studio
```

Add to `/etc/profile`:

```bash
export ANDROID_HOME=/opt/android/sdk
export ANDROID_SDK_HOME =/opt/android/sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```
