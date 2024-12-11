---
layout: default
title:  "My notes on NixOS installation"
last_modified_at:   2024-10-31 8:30:00 +0000
---

Just some notes :D

Lets go to the plan for the whole system structure :D

| Partition | Filesystem | Mountpoint | Subvolume | Compress (level) |
|-----------|------------|------------|-----------|-----------|
| /dev/sda1 | FAT32       | /boot/efi   |    -       |  -       |
| /dev/sda2 | btrfs       | /      | root, home|    zstd (1:5)  |        


Create root partition 
```sh
mkfs.btrfs /dev/sda2
```
Mount the root partition 
```sh
mount /dev/sda2 /mnt
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
mount -o compress=zstd,subvol=root /dev/sda2 /mnt
mount -o compress=zstd,subvol=home /dev/sda2 /mnt/home
mount /dev/sda1 /mnt/boot
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

# Sharing is caring!
<a id="threads-share" href="#" target="_blank">
  <img src="https://img.shields.io/badge/Share_on-Threads-black?style=for-the-badge&logo=threads" alt="Share on Threads">
</a>

<a id="instagram-share" href="#" target="_blank">
  <img src="https://img.shields.io/badge/Share_on-Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Share on Instagram">
</a>

<a id="twitter-share" href="#" target="_blank">
  <img src="https://img.shields.io/badge/Share_on-Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white" alt="Share on Twitter">
</a>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    var currentURL = window.location.href;
    document.getElementById('threads-share').href = 'https://www.threads.com/share?text=Check%20this%20out!&url=' + encodeURIComponent(currentURL);
    document.getElementById('instagram-share').href = 'https://www.instagram.com/sharer.php?u=' + encodeURIComponent(currentURL);
    document.getElementById('twitter-share').href = 'https://twitter.com/share?url=' + encodeURIComponent(currentURL) + '&text=Check%20this%20out!';
  });
</script>

