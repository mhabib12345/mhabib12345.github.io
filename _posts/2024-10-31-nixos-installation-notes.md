---
layout: default
title:  "My notes on NixOS installation"
---

Just some notes :D

Create root partition 
```sh
mkfs.btrfs /dev/vda2
```
Mount the root partition 
```sh
mount /dev/vda2 /mnt
```
Create btrfs subvolume ( home and root)
```sh
btrfs create subvolume /mnt/home
btrfs create subvolume /mnt/root
umount /mnt
```
Create mountpoint and mount the partition respectively 
```sh
mkdir /mnt/boot
mkdir /mnt/home
mount -o compress=zstd,subvol=root /dev/vda2 /mnt
mount -o compress=zstd,subvol=home /dev/vda2 /mnt/home
mount /dev/vda1 /mnt/boot
```
Generate the config and copy it to the root partition 
```sh
nixos-generate-config --root /mnt
```
"EDIT"

Start the installation process 
```sh
nixos-install
```