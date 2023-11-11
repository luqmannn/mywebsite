---
title: Things To Do After Installing Fedora 38

date: 2023-10-29
type: page
categories:
    - Linux
tags:
    - Bash
    - Fedora
---

Check out the [previous post](https://luqmannn.xyz/tutorial/things-to-do-fedora-37/) where I explained in detail, I don't want to repeat myself. With the release of Fedora 38, I decided to install the operating system in my laptop MSI Modern 14, an entry level laptop that I bought few months ago. Here's the specification below:

```
Host: Modern 14 C11M REV:1.0
CPU: 11th Gen Intel i3-1115G4 (4) @ 4.100GHz 
GPU: Intel Tiger Lake-LP GT2 [UHD Graphics G4] 
Memory: 7630MiB
Storage: Micron_2400_MTFDKBA512QFM 512GB NVMe SSD
```

> I copy the spec from neofetch and lshw command.

### Configure DNF package manager
```
printf "%s" "
max_parallel_downloads=7
fastestmirror=true
" | sudo tee -a /etc/dnf/dnf.conf
```
> I didn't set `deltarpm=true` simply because it will eat more cpu resources in order to compress the download file into smaller size but this has failed few times. I'd say the the smaller file size was negligable.

### Update the entire system 
```
sudo dnf update
```

### Enable RPM fusion free and non-free repo
```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf group update core
```

### Debloat
```
sudo dnf remove gnome-online-accounts gnome-text-editor gnome-maps gnome-software ffmpeg-free libswscale-free libreoffice* video rhythmbox totem
```

### Run firmware updates
> Make sure to plug-in the laptop first before running the command below.
```
sudo dnf autoremove
sudo fwupdmgr get-devices
sudo fwupdmgr refresh
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

### Add Flathub repository
```
sudo dnf install fedora-flathub-remote
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### Install extra software
```
sudo dnf install jetbrains-mono-fonts-all unrar unzip lshw neofetch tldr ffmpeg mpv yt-dlp libexif gsmartcontrol gnome-tweaks telegram-desktop
```

#### Codium
```
sudo rpmkeys --import https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg
printf "[gitlab.com_paulcarroty_vscodium_repo]\nname=download.vscodium.com\nbaseurl=https://download.vscodium.com/rpms/\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg\nmetadata_expire=1h" | sudo tee -a /etc/yum.repos.d/vscodium.repo
sudo dnf install codium
```

#### Ani-cli
```
sudo dnf copr enable derisis13/ani-cli
sudo dnf install ani-cli
```

### Configure GNOME
```
gsettings set org.gnome.desktop.a11y always-show-universal-access-status true
gsettings set org.gnome.desktop.wm.preferences button-layout 'appmenu:minimize,maximize,close'
gsettings set org.gnome.desktop.interface clock-show-weekday true
gsettings set org.gnome.desktop.interface clock-show-seconds true
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
```
