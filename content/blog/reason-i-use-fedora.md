---
title: The Real Reason I Use Fedora
type: page
description: Reason I Use Fedora
topic: blog
---

The reason might be different than what most people expected. At first, I used Arch Linux installed as my main operating system. It was a great experience as the system is not only minimal, but as a user, you install only the packages that you want. So there are no unnecessary things running in the background. Then, I wanted to use a virtualization software and set up a Windows 10 virtual machine using QEMU/KVM Virt-Manager, because I wanted to switch from Virtualbox and VMware Workstation. Virt-Manager is a far superior virtualization software for Linux distributions because it uses the KVM module that is contained in the Linux kernel to do its job, unlike other virtualization software that runs on the software level. It took some time to learn the interface and certain functions that I had never heard of before.

Then, I began to load the Windows ISO and virt-io image file to Virt-Manager and started installing Windows 10. At some point during the installation, the virtual machine would hang after reaching 90-93% progress. Thinking about what I did wrong this time, I immediately deleted the virtual machine, started the installation, and the same thing happened again three times. Nevertheless, I calmed myself down and thought about the problem. Without any reason, I started to check the storage size of every partition and found the root cause. Why had Arch decided to give my /home partition such a large size, while neglecting the root partition with only 20GB? That is unacceptable.

Partition | Size
--------- | -----
/		| 20GB
/home	| 210GB
/boot	| 600MB
Zram	     | 8GB


I began scratching my head, trying to figure out how to increase the size of the root partition using the excess size of the home partition. In other words, I needed to resize the root partition, preferably with more storage space, without accidentally nuking the system. Because I needed to resize the root partition, the process needed to be done using a live bootable USB containing a Linux distribution with a partitioning tool such as Gparted. I also learned that in order to do this, I needed to first deactivate the swap partition and arrange it to the last block in the partition table. Then, the second question arose: how do I turn off the swap partition, if it doesn't even have that partition in the first place, but instead uses something called zram?

I don't really know why Arch needs to allocate more than one GB of storage size to zram. I think it's unnecessary since PCs/laptops are more capable than ever before. But from a technical standpoint, I might be wrong. To disable zswap permanently, add `zswap.enabled=0` to your kernel parameters located in the GRUB bootloader file, `/etc/default/grub`. Go to the line `GRUB_CMDLINE_LINUX_DEFAULT` and add the value `zram.enabled=0` after the other parameters, separated by a space. Save the file and exit, then update the GRUB config file using the command below:

`sudo mkconfig -o /boot/grub/grub.cfg`

I rebooted the system and checked the partition using the lsblk command and there was still zram there. Using these two commands below, I was able to disable it again, either by rebooting or running:

```
sudo swapoff /dev/zram0
sudo rmmod zram
```

But this still didn't solve my problem with partitioning. I booted back to the Linux bootable USB and found out that zram was activate back every time the PC/lptop on. I'm dissapointed by the outcome that I cannot resize root partition because of this reason. I learned my lesson here that partitoning is not something to be taken lightly as a Linux user and especially very important to system administrator when setting up the system or server. You need to allocate enough partition to both root and home partition respectively without neglecting the other. After that, I nuke my Arch installation and use Fedora 37 as my main operating system. Hopefully this time, there's nothing major need to be worried and I can be at peace with my system.
