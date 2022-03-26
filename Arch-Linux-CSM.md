# Arch Linux on VMware Workstation Player Version: 16

## Table of contents

- [Pre-Installation](#Pre-Installation).
  - [Setting up VMwareworkstation player](#Setting-up-VMwareworkstation-player)
  - [Set the console keyboard layout](#Set-the-console-keyboard-layout)
  - [Update the system clock](#Update-the-system-clock)
  - [Partition the disks](#Partition-the-disks)
  - [Format the partitions](#Format-the-Partitions)
  - [Mount the file systems](#Mount-the-file-systems)
- [Installation](#Installation)
  - [Install essential packages](#Install-essential-packages)
- [Configure the system](#Configure-the-system)
  - [Fstab](#Fstab)
  - [Chroot](#Chroot)
  - [Time zone](#Time-zone)
  - [Install text-editor](#Install-text-editor)
  - [Localization](#Localization)
  - [Setting up Host Name](#setting-up-Host-Name)
  - [Package Manager Configuration](#Package-Manager-Configuration)
  - [Setting Root password](#Setting-Root-password)
  - [Install sudo](#Install-sudo)
  - [Add normal user](#Add-normal-user)
  - [Configuring Boot loader](#Configuring-Boot-loader)
  - [Networking configuration](#Network-configuration)
  - [Completed](#Completed)
- [Installing display server Xorg](#Installing-display-server-Xorg)
  - [Driver installation](#Driver-Installation)
- [Installing window manager i3-wm](#Installing-window-manager-i3-wm)
- [Installing display manager](#Installing-display-manager)
  - [Set default LightDM greeter](#Set-default-LightDM-greeter)
  - [Start and Enable LightDM](#Start-and-Enable-LightDM)
- [Installing VMWare Tools](#Installing-VMWare-Tools)

## Pre-Installation

### Setting up VMwareworkstation player

- Start Vmware Workstation
- Create New Virtual Machine
- Installer Disk Image -> Browse to and select correct ISO
- Linux -> Other Linux 5.x and later kernel 64-bit (5.10)
- Select name and folder
- Set disk size as per your requirement
- Set RAM size as per your requirement
- Set Number of processor cores as per your requirement
- Play Virtual Machine

### Set the console keyboard layout

The default console keymap is US. Available layouts can be listed with:

```
ls /usr/share/kbd/keymaps/**/*.map.gz | less
```

To modify the layout, append a corresponding file name to loadkeys. omitting path and file extension.

```
loadkeys fr-latin1
```

### Update the system clock

Use timedatectl(1) to ensure the system clock is accurate

- Use the following to find your time zone

```
timedatectl list-timezones | less
```

- To set your time zone for example Asia/Kolkata

```
timedatectl set-ntp true
timedatectl set-timezone Asia/Kolkata
```

- To check the service status, use `timedatectl status`.

### Partition the disks

```
cfdisk /dev/sda
```

- Select label type as gpt
- Create new Partiiton size of 1M where Type is `BIOS boot`.
- Create new Partition size of 4G commonly (1.5 x RAM) where Type is `Linux swap`.
- Create new partion size of the remaining size where Type is `Linux filesystem`.
- Write and Quit.

### Format the Partitions

Once the partitions have been created, each newly created partition must be formatted with an appropriate **file system**.

- To make a swap Partition

```
mkswap /dev/sda2
swapon /dev/sda2
```

- To format big Partition to ext4

```
mkfs.ext4 /dev/sda3
```

### Mount the file systems

Mount the file systems

```
mount /dev/sda3 /mnt
```

## Installation

### Install essential packages

```
pacstrap /mnt base linux linux-firmware
```

## Configure the system

### Fstab

Generate an fstab file (use -U or -L to define by UUID or labels, respectively):

```
genfstab -U /mnt >> /mnt/etc/fstab
```

### Chroot

- Change root into the new system:

```
arch-chroot /mnt
```

### Time zone

- Set the time zone: `ln -sf /usr/share/zoneinfo/Region/City /etc/localtime`

```
ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
```

- Run hwclock(8) to generate /etc/adjtime:

```
hwclock --systohc
```

### Install text-editor

```
pacman -S vim
```

### Localization

```
vim /etc/locale.gen
```

**Edit** /etc/locale.gen and uncomment `en_US.UTF-8 UTF-8` and other needed locales.

- Generate the locales by running:

```
locale-gen
```

### Setting up Host Name

- Creating hostname

```
vim /etc/hostname
```

- give your host a name

- for example VMWareArchLinux

```
VMWareArchLinux
```

- Write & quit

### Package Manager Configuration

This step in _optional_ multilib allow us to install 32-bit packages.

- To edit pacman.conf

```
vim /etc/pacman.conf
```

- Uncomment the following

```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

- Write & Quit

- To sync repo

```
pacman -Syyu
```

### Setting Root password

- Set the root **password**:

```
passwd
```

### Install sudo

```
pacman -S sudo
```

### Add normal user

- Add user

```
useradd -m [userName]
```

- create passwd for [userName]

```
passwd [userName]
```

### Add user to sudoers

```
EDITOR=vim visudo
```

- Uncomment the following line `%wheel ALL=(ALL:ALL) ALL`

```
 usermod -aG wheel,audio,video,optical,storage [userName]
```

### Configuring Boot loader

```
pacman -S grub
```

- Installing grub to proper partition

```
grub-install /dev/sda
```

- Configuring grub

```
grub-mkconfig -o /boot/grub/grub.cfg
```

### Networking configuration

```
pacman -S networkmanager
```

- Enable NetworkManager

```
systemctl enable NetworkManager
```

### Completed

- Exit from Chroot

```
exit
```

- Reboot the system

```
reboot
```

## Installing display server Xorg

### Driver installation

- First, identify the graphics card

```
lspci -v | grep -A1 -e VGA -e 3D
```

- Then, install an appropriate driver. You can search the package database for a complete list of open-source video drivers:

```
pacman -Ss xf86-video
```

- Install proper driver for VMWare _(On physical machines, install the appropriate driver for intel, amd or nvidia. Check the wiki.)_

```
sudo pacman -S xf86-video-vmware
```

- Installing xorg

```
sudo pacman -S xorg xorg-server
```

## Installing window manager i3-wm

```
sudo pacman -S i3-wm i3status terminator
```

## Installing display manager

- Installation of lightdm

```
sudo pacman -S lightdm
```

- After successfully installing LightDM, you may want to install LightDM greeter as well. A greeter is a GUI that prompts the user for credentials, lets the user select a session, and so on.

```
sudo pacman -S lightdm-gtk-greeter
```

### Set default LightDM greeter

- To set a default greeter for your Arch LightDM, edit the file `/etc/lightdm/lightdm.conf`.

```
sudo vim /etc/lightdm/lightdm.conf
```

- Then the line in the file we look something like this:

```
[Seat:*]
...
greeter-session=lightdm-gtk-greeter
```

### Start and Enable LightDM

- On Arch, LightDM service is controlled by systemd. The name of the service is lightdm.service. To start the service and set it to start on boot, run:

```
systemctl enable lightdm.service
```

- Reboot your system

## Installing VMWare Tools

- Install git

```
sudo pacman -S git
```

- Installation of open-vm-tools

```
git clone https://github.com/rasa/vmware-tools-patches.git
```

```
cd vmware-tools-patches
```

```
sudo ./patched-open-vm-tools.sh
```
