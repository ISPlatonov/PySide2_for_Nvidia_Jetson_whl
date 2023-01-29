# UPGRADE UBUNTU ON JETSON NANO (18.04 -> 20.04)

**IMPORTANT! Working with Ubuntu 18.04 (JetPack 4)!**

There is a `do-release-upgrade` command to upgrade, but before that you need to change the upgrade policy.

Change the file `/etc/update-manager/release-upgrades`:

```shell
[DEFAULT]
Prompt=lts
```

Before updating directly, you must remove chromium and then update all existing packages:

```shell
sudo apt remove --purge chromium-browser chromium-browser-l10n -y

sudo apt update
sudo apt upgrade -y
```

If you asked about restarting docker, we do it.

Next, run the update command:

```shell
sudo do-release-upgrade --allow-third-party
```

You must confirm each question by typing `y`. The update has started and can take up to 8 hours, so if it's being done remotely (via ssh), you'll need to turn off screen fading and hibernation.

When finished, reinstall some packages:

```shell
sudo apt install --reinstall libappstream* -y
sudo apt install fwupd fwupdate -y
```

Next, comment out the lines in the `/etc/apt/apt.conf.d/50appstream` file (the lines may differ a bit, but most likely they will be the same and be located at the end of the file):

```shell
...
# APT::Update::Post-Invoke-Success {
# "if /usr/bin/test -w /var/cache/app-info -a -e /usr/bin/appstreamcli; then appstreamcli refresh-cache > /dev/null | true; fi";
# };
```

Remove some packages:

```shell
sudo apt remove vpi1-samples
```

And update the remaining packages:

```shell
sudo apt update
sudo apt upgrade -y
```

[Set up VNC for remote access again](https://developer.nvidia.com/embedded/learn/tutorials/vnc-setup)

It is also important to set autologin for remote access, so in the `/etc/gdm3/custom.conf` file we change the lines:

```shell
...

# Enabling automatic login
   AutomaticLoginEnable=true
   AutomaticLogin = jetson

...
```

Restart Jetson:

```shell
sudo reboot
```

You can update the packages again:

```shell
sudo apt update
sudo apt upgrade -y
```

And here is Jetson on Ubuntu 20.04!

After that, you can install PySide2, see [INSTALL_PYSIDE2.md](INSTALL_PYSIDE2.md).