---
title: Arch Linux Installation Experience: Starting from Scratch
---

# Arch Linux Installation Experience: Starting from Scratch

In the vast world of Linux, choosing the right distribution is a journey every enthusiast must embark on. Recently, I took on the challenge of installing Arch Linux on one of my computers—a distribution known for its simplicity, modernity, and flexibility. Unlike many other popular distributions, Arch requires the user to manually configure the system from the ground up, presenting both a challenge and a fantastic opportunity to delve deeper into Linux. This blog aims to provide a detailed guide to installing Arch Linux, with a special emphasis on partitioning, mounting, and network configuration. I will closely follow the [official documentation](https://wiki.archlinux.org/title/installation_guide) to ensure a smooth installation process.

## Introduction

Arch Linux is favored by many advanced users for its rolling release model, extensive official repositories, and the AUR (Arch User Repository). However, its installation process can seem daunting due to its manual nature. From creating a bootable drive to system configuration, each step requires careful attention and a certain level of technical knowledge. My goal is to create a guide that includes only the essential steps to help you navigate this process.

## Preparing the Bootable Medium

First, you'll need an Arch Linux installation medium. I recommend using the ISO file provided by the official website to create a bootable USB drive. Insert the USB into your computer and boot up. You will enter the Arch installation environment after adjusting your BIOS settings to boot from the USB. This live system allows you to detect and prepare your hardware before installing Arch Linux.

### Display Settings

#### Setting the Font

If the default font is too small, you can use the `setfont sun12x22` command to set a larger font, which is very helpful for protecting your eyes. `ter-132b` is another good choice.

#### Adjusting Brightness

For laptop users, you may need to adjust the screen brightness depending on your hardware. The Arch Wiki provides a very detailed [brightness adjustment guide](https://wiki.archlinux.org/title/Backlight).

#### Updating the System Clock

Use the `timedatectl set-ntp true` command to ensure the system clock is accurate.

### Partitioning and Mounting

Disk partitioning is a key step in the installation process. I strongly recommend using the UEFI boot mode as it's the standard for modern hardware. Use `wipefs --all /dev/<device>` to clear the disk, then `cfdisk /dev/<device>` for partitioning. In cfdisk, you can create an EFI system partition and a root partition as needed, selecting the correct partition types.

Mounting the partition is the next step. Make sure you have formatted the partitions (e.g., using `mkfs.ext4` for the root partition) before mounting them to the installation point.

### Bootstrapping the System and Configuring the Network

#### Installing the Basic System

Use the `pacstrap` tool to install the basic system and necessary packages to your root partition. A typical command is `pacstrap -K /mnt base linux linux-firmware base-devel`.

#### Generating fstab

Run `genfstab -U /mnt >> /mnt/etc/fstab` to automatically generate the `fstab` file, which is crucial for automatically mounting partitions at system startup.

#### Chroot and Networking

`arch-chroot /mnt` to enter your new system. At this point, installing `networkmanager` and enabling it with `systemctl enable NetworkManager` is crucial so you can easily connect to the network after rebooting.

### Post-Installation Configuration

#### Creating Users and Connecting to the Network

In Arch Linux, you need to log in as the root user initially. For safety, it's a good practice to create a regular user and assign the necessary permissions. Remember to install `sudo` and configure the `/etc/sudoers` file. Connecting to the network is usually as simple as using the `nmtui` command.

## Conclusion

Congratulations, you have successfully installed Arch Linux and performed the basic configuration! While the installation process of Arch might seem intimidating at first glance, it actually offers an excellent learning opportunity, allowing you to understand how your system works in depth. Through this process, you have not only installed an operating system but also gained valuable knowledge and skills. I hope this guide helps you smoothly complete the installation of Arch Linux and enjoy the limitless possibilities that Arch brings!
