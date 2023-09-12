# dwm on ubuntu server

> [!TODO] TODOs for htc
> - Wallpaper: `w01.jpg` (for screen) and `w02.jpg` (for konsole)
> - `nerdfonts.sh`
> - `.vimrc`

```sh
sudo apt update
sudo apt install git micro neofetch unzip konsole
```

```sh
# set timezone
timedatectl
sudo timedatectl set-timezone Asia/Saigon

# Font for console: Terminus
sudo dpkg-reconfigure console-setup
```

## dwm

```sh
# some basic dependencies need to install
sudo apt install build-essential xorg libx11-dev libxft-dev libxinerama-dev
```

```sh
mkdir suckless
cd suckless
git clone https://git.suckless.org/dwm
git clone https://git.suckless.org/dmenu
git clone https://git.suckless.org/st
git clone https://git.suckless.org/slstatus

# build dwm
cd dwm
sudo rm config.h # if exit
cp config.def.h config.h  
micro config.h
# replace default terminal `st` by `konsole`
sudo make clean install

# build st
cd ../st
sudo make clean install

# build dmenu
cd ../dmenu
sudo make clean install

# build slstatus
cd ../slstatus
sudo make clean install

echo "exec dwm" >> ~/.xinitrc
# to make the `.xinitrc` file executable
chmod +x ~/.xinitrc

echo "startx" >> ~/.bash_profile
sudo reboot
```

- Them vao file *.xinitrc*:

```sh
micro .xinitrc

# Display Resolution
xrandr --output Virtual1 --mode 1920x1080 &
```

**NOTE:** add the below to `~/.profile` to set **screen resolution** for DWM in case install *kde-plasma-desktop*

```
xrandr --output Virtual1 --mode 1920x1080 &
```

```sh
sudo apt update

sudo apt install -y curl pcmanfm dolphin feh

micro .xinitrc
# set screen wallpaper 
feh --bg-fill ~/Pictures/wallpaper/w01.jpg &

# create folders (Documents, Downloads...)
xdg-user-dirs-update
```
## Install applications

```sh
sudo apt install chromium

# https://obsidian.md/download
sudo apt install ./obsidian_1.4.5_amd.deb

# https://www.google.com/chrome/
cd Downloads
sudo apt install ./google-chrome-stable_current_amd64.deb

sudo apt install -y vim
```

**install vim/plugged:** https://github.com/junegunn/vim-plug
Reload .vimrc and `:PlugInstall` to install plugins.


```sh
# install fonts
sudo apt install fonts-recommended fonts-terminus

# install nerdfonts.sh file
# unzip package requirement
chmod +x nerdfonts.sh
./nerdfonts.sh

# Sound packages
sudo apt install -y pulseaudio pavucontrol
```

```sh
sudo apt install -y network-manager
sudo apt install -y sxhkd
mkdir ~/.config/sxhkd
```

## Flatpak 👈

```sh
sudo apt install flatpak

# Add the Flathub repository
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

sudo reboot
```

## FreeFileSync

```sh
#unzip file
sudo tar xvzf FreeFileSync_12.5_Linux.tar.gz

# Installation directory:   /opt/FreeFileSync
```

## Tor browser – Using Manual Tarball file

- https://www.torproject.org/download/
- https://vegastack.com/tutorials/how-to-install-tor-browser-on-ubuntu-22-04/

```sh
cd ~/Downloads
tar -xvf tor-browser-linux64-*.tar.xz
cd tor-browser/

# For Application launcher shortcut:
./start-tor-browser.desktop --register-app
```

## Calibre is 6.25.0.

https://calibre-ebook.com/download_linux

```sh
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

# Run "calibre" to start calibre
```

## Zotero

**Zotero 6 for Linux** and **Zotero Connector**
- https://www.zotero.org/download/
- https://www.zotero.org/support/installation#installation_instructions

```sh
# To extract files in a defend location, use `**-C**` option followed by the destination directory
tar -xvjf filename.tar.bz2 -C /opt
```

```sh
# to extract a `.tar.bz2` file:
tar -xjf filename.tar.bz2
```

**Download the Zotero Tarball file**

```sh
wget "https://www.zotero.org/download/client/dl?channel=release&platform=linux-x86_64" -O zotero64.tar.bz2

# Extract file
tar -xf zotero64.tar.bz2

# move it to /**opt** directory:
sudo mv Zotero_linux-x86_64 /opt/zotero

# Create a Desktop shortcut
cd /opt/zotero
sudo ./set_launcher_icon

# For Application launcher shortcut:
sudo ln -s /opt/zotero/zotero.desktop ~/.local/share/applications/zotero.desktop

# For Desktop shortcut
ln -s /opt/zotero/zotero.desktop ~/Desktop/zotero.desktop

# Allow Desktop  shortcut launching:
# - Right-click on the icon appearing on your desktop and select “Allow Launching“.
```

## Miniconda

**Method 1 -** [Download the installer.](https://docs.conda.io/projects/miniconda/en/latest/index.html)
- https://docs.conda.io/projects/miniconda/en/latest/miniconda-install.html

**Method 2 - Quick command line install**

```sh
# These four commands quickly and quietly install the latest 64-bit version of the installer and then clean up after themselves.
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh

# After installing, initialize your newly-installed Miniconda. The following commands initialize for bash and zsh shells:
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh

conda --version
# conda 23.5.2 with Python 3.11.4
```

**to configure conda-forge as your default package channel**

```sh
# (base) $ 
conda config --add channels conda-forge
conda config --set channel_priority strict
```

**create a new conda “environment”**

- [[python environments and conda environments]]

```sh
(base) $ conda create -y -n pydata python=3.10

# activate the environment
conda activate pydata
```

**install the essential packages**

```
conda install -y numpy pandas jupyter matplotlib

conda install -y lxml beautifulsoup4 html5lib openpyxl

conda install -y requests sqlalchemy seaborn scipy statsmodels

conda install -y patsy scikit-learn pyarrow pytables numba
```

**NOTE:** all above have been installed for *pydata* environment

## VSCode

 https://code.visualstudio.com/download

```sh
sudo apt install ./code_1.81.1-1691620686_amd64.deb
```

## Some references

```sh
sudo micro /usr/share/xsessions/dwm.desktop
```

add to `dwm.desktop`

```
[Desktop Entry]
Encoding=UTF-8
Name=dwm
Comment=Dynamic window manager
Exec=dwm
Icon=dwm
Type=XSession
```

**NOTE:** enter konsole and create new profile
- *konsole config* file: `~/.config/konsolerc`

## install MS fonts

```sh
# Install MS fonts for Debian 12
sudo apt update && sudo apt upgrade
sudo apt-add-repository contrib non-free -y
sudo apt install software-properties-common -y
sudo apt install ttf-mscorefonts-installer

# Install MS fonts for Ubuntu
sudo apt update && sudo apt install ttf-mscorefonts-installer

sudo fc-cache -f

# OR
sudo fc-cache -f -v

# check
fc-match Arial
```

## network shares

```sh
sudo apt update
sudo apt install dolphin

# https://markontech.com/linux/mount-a-network-shared-drive-on-linux/
# to mount and manage network shares
sudo apt install cifs-utils

# Creating A Mount Point
sudo mkdir /mnt
sudo mkdir /mnt/share
sudo mount.cifs //192.168.1.21/Tb /mnt/share/ -o user=usernamehere,pass=passwordhere
# network share does not have credentials to access
sudo mount.cifs //192.168.1.21/Tb /mnt/share/
```

Mount Permanently And Automatically On Boot
- [!] **!!!PLEASE PAY ATTENTION ON THIS STEP!!!**

**If you don’t do it properly, you could lock up your machine on the next restart**. Fstab file is the boot process configuration file which has your HDD’s in it as well. So, if the file is not configured properly, you could prevent the machine from booting.

```sh
sudo -s nano /etc/fstab
```

**AT THE BOTTOM OF THE FILE** add the following line:

```sh
//192.168.1.21/Tb /mnt/share/ cifs username=usernamehere,password=passwordhere 0 0
```

