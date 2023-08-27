---
title: Things To Do After Installing Fedora 37

date: 2023-06-11
type: page
categories:
    - Linux
tags:
    - Bash
    - Fedora
---

## Configure DNF package manager
Open the DNF config file using the command below
```{sh}
sudo vim /etc/dnf/dnf.conf
```
DNF can simultaneously downloads package for faster install and update process. By defaults, DNF set parallel downloads to 3. Maximum of 20. You can set it depends on your internet connection speed. Some of the setting below is self explainatory like fastest mirror. For deltarpm, it is something that DNF use to save bandwidth by downloading much smaller delta RPM files to rebuild them locally. However, this is quite CPU and I/O intensive. By default, it is true

- Add the parameter to the file, then save the file and exit
```{sh}
max_parallel_downloads=6
fastestmirror=yes
deltarpm=yes
```
- Or you use one-liner command down below
```{sh}
sudo sh -c 'echo "max_parallel_downloads=6\nfastestmirror=yes\ndeltarpm=yes" >> /etc/dnf/dnf.conf'
```

### Enable RPM Fusion free and non-free repo
By default, Fedora adheres strictly to their principle by shipping only free and open soure software (FOSS) in their Linux distribution to avoid software encumbered by patents. Some FOSS doesn't available by default but available in RPM Fusion free repository that comply with Fedora's licensing policies. While the RPM Fusion non-free repository provides software packages that do not comply with Fedora's licensing policies such as proprietary NVIDIA graphics card drivers, multimedia codecs like FFmpeg and miscellaneous software like Steam which we'll install later. To enable RPM Fusion free and non-free repository, use the command below.
```{sh}
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

## Update the entire system
It is self explainatory, basically it refresh all the package index database to the latest including the one we configure earlier and download all the latest software installed in Fedora including the kernel in one-single command. 
```{sh}
sudo dnf update
```

### Install proprietary Nvidia drivers (only required for when you have an Nvidia GeForce GPU)
If you somehow skip the earlier step, use both of the command below. If not, then no worries you only need to install the driver using the second command only because the RPM non-free repo already enabled.
```{sh}
sudo dnf config-manager --set-enabled rpmfusion-nonfree-nvidia-driver
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
```

## Install some software
### VSCodium
It depends on your use case and what software to install. In this case I'm using VSCodium, so we need to add the GPG key of VSCodium repository to Fedora-based system and install the software.
```{sh}
sudo rpmkeys --import https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg
printf "[gitlab.com_paulcarroty_vscodium_repo]\nname=download.vscodium.com\nbaseurl=https://download.vscodium.com/rpms/\nenabled=1\ngpgcheck=1\nrepo_gpgcheck=1\ngpgkey=https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/-/raw/master/pub.gpg\nmetadata_expire=1h" | sudo tee -a /etc/yum.repos.d/vscodium.repo
sudo dnf install codium
```

### Add Flathub repository
By default, Flathub repository is already enabled in Fedora Workstation. But if it is not enabled, you can easily add it using the command below
```{sh}
sudo dnf install fedora-flathub-remote
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### Search and install Flatpak application
Flatpak is the primary way that apps can be installed on Fedora Silverblue, but it can also be used to install application on Fedora Workstation. One of the reason to use Flatpak is simply to avoid package breakage and maintain package stability by including almost any dependency or library as part of their application. All Flatpak application can be easily search from the terminal using `flatpak search application_name`. To install the application, run `flatpak install flathub application_id`. In this example, I'll use Discord, Spotify, Joplin, Lossless Cut
```{sh}
flatpak install flathub com.discordapp.Discord com.spotify.Client net.cozic.joplin_desktop no.mifi.losslesscut
```

### Manage Flatpak applications
Flatseal is a graphical utility to review and modify permissions from your Flatpak applications. It give us the ability control every single permission to access system resources with a toggle just like in Android.
```{sh}
flatpak install flathub com.github.tchx84.Flatseal
```

## Customization
### Install GNOME Tweaks and Extension Manager
#### GNOME Tweks
```{sh}
sudo dnf install gnome-tweaks
```
#### Extension Manager
A utility for browsing and installing GNOME Shell Extensions. It also has features that enable user to browse `extensions.gnome.org` right inside the app and manage the extensions you already have installed
```{sh}
flatpak install flathub com.mattjakeman.ExtensionManager
```

## Miscellaneous
### Fix mpv doesn't play mp4 and Hi10-bit H265 mkv video very well (stuttering), use at your own risk!

- The mp4 video played poorly when I want to immediately skip to other timestamp, sometimes video goes out of sync with audio while Hi10-bit H265 mkv video goes full black screen with only audio being played.
- I uninstalled proprietary drivers (**NOT** recommended if using Nvidia), restart and install `ffmpeg`, at first dnf throw some error
```
Error: 
 Problem: problem with installed package libswscale-free-5.1.2-1.fc37.x86_64
  - package ffmpeg-libs-5.1.2-3.fc37.x86_64 conflicts with libswscale-free provided by libswscale-free-5.1.2-1.fc37.x86_64
  - package ffmpeg-5.1.2-3.fc37.x86_64 requires ffmpeg-libs(x86-64) = 5.1.2-3.fc37, but none of the providers can be installed
  - conflicting requests
```

```{sh}
sudo dnf remove ffmpeg-free
sudo dnf remove libswscale-free
sudo dnf install jetbrains-mono-fonts-all neofetch tldr ffmpeg mpv gsmartcontrol perl-Image-ExifTool yt-dlp telegram-desktop
```
- Mpv need some of the dependencies provided by `ffmpeg` in order to work properly.
- In order to install `ffmpeg` you need to add RPM Fusion repositories since Fedora ship with only open source packages without any proprietary codecs or driver.
- `libswscale-free` package came along with `ffmpeg-free`, which cause conflict with `ffmpeg`. That's why we need to remove both of them.

#### Conclusion
1. It looks like that `mpv` need some of the dependencies provided by `ffmpeg` in order to work properly.
2. `libswscale-free` package came from the proprietary drivers along with `ffmpeg-free`, which cause conflict with `ffmpeg`.
3. I remove RTX 2060 graphic card from my system and didn't even bother to install proprietary drivers anymore since open source drivers works fine.

> I don't want to trigger any more issue since it is my main system and I've been troubleshooting this issue for almost one and a half day straight.

- Also, I decided to dig deeper about the issue and guess what, some user face almost similar issue like me:
	- [Mpv does not work with Nvdec](https://forums.developer.nvidia.com/t/525-53-mpv-does-not-work-with-nvdec/233691)


### Setting up for virtualization
- Check for virtualization support
`LC_ALL=c lscpu | grep Virtualization`
- Edit libvirtd permission
`sudo vim /etc/libvirt/libvirtd.conf`
- Enable the line below by uncomment, then save the file and exit
```{sh}
unix_sock_group = "libvirt"
unix_sock_ro_perms = "0777"
unix_sock_rw_perms = "0770"
```

To installs the virtualization software package from the DNF package manager, the "@" symbol indicates that the package is a group package, which installs multiple packages at once. In this case, it installs the necessary packages for virtualization.Then we need to adds the user specified by "username" to the "libvirt" group. This is necessary to allow the user to manage virtual machines. Then, enables the "libvirtd" service to start automatically at boot and starts the service immediately.
```{sh}
sudo dnf install @virtualization
sudo usermod -aG libvirt username
sudo systemctl enable --now libvirtd
```