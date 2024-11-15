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
<!-- Twitter Share Button -->
<button id="shareOnTwitter">Share on Twitter</button>

<script>
  document.getElementById('shareOnTwitter').addEventListener('click', function() {
    // Get the current page's URL
    const pageUrl = encodeURIComponent(window.location.href);
    // Define your tweet text
    const tweetText = encodeURIComponent("Check this out!");

    // Open Twitter's share URL in a new window
    const twitterShareUrl = `https://twitter.com/intent/tweet?url=${pageUrl}&text=${tweetText}`;
    window.open(twitterShareUrl, '_blank');
  });
</script>
