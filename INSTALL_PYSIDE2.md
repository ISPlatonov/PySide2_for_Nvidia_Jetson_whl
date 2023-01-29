# Install PySide2 (Qt 5.12) on Jetson Nano

**Important! Working with** [**Ubuntu 20.04**](UPGRADE_UBUNTU.md)**!**

Since there is no official PySide2 build for ARM processors, we will use a pre-built package. It needs a version of `Python==3.6` to work properly, so let's start by installing the correct version; add the `deadsnakes` package archive, then install via the package manager:

```shell
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.6
```

After that, you need to make several connections:

```shell
sudo ln -s /usr/lib/python3/dist-packages/apt_pkg.cpython-{38,36m}-aarch64-linux-gnu.so

cd /usr/lib/python3/dist-packages/gi
sudo git clone https://github.com/ISPlatonov/Python*36m_aarch64_gi_.so*files.git
sudo cp Python*36m_aarch64_gi_.so_files/*gi* .
```

You can update packages:

```shell
sudo apt update
sudo apt upgrade -y
```

Finally select `python3.6`:

```shell
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 2

sudo update-alternatives --config python3

sudo update-alternatives --set python /usr/bin/python3.6
```

To check, type `python3 -V` - it should display the version `Python 3.6.x`.

Now you can install PySide2:

```shell
cd
git clone https://github.com/ISPlatonov/PySide2*for_Nvidia_Jetson*whl
cd PySide2*for_Nvidia_Jetson*whl
pip3 install *.whl
```

If there were no errors, PySide2 is installed on the system as a python package.