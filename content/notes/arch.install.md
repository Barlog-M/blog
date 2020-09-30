+++
title = "Arch Linux. Installation notes"
date = 2020-09-30
+++

There is a very good [Installation guide](https://wiki.archlinux.org/index.php/Installation_guide). But it contains a lot of links to other articles. And here i collected some useful notes for Arch Linux installation process.

### Install essential packages

I use Linux Zen

Benefits of Linux ZEN (**liquorix** is binary of ZEN for Debian) [liquorix](https://liquorix.net)

```bash
$ pacstrap /mnt base linux-zen linux-zen-headers linux-firmware
```

### Rebuild kernel

```bash
$ mkinitcpio -p linux-zen
```

### Software RAID

1. In file **/etc/mkinitcpio.conf** add module `mdadm_udev` to HOOKS property

2. Add RAID config to **/etc/mdadm.conf**

    `ARRAY /dev/md/0 metadata=1.2 UUID=225393cd:9b57f03f:ac2bc0f3:e8379bab name=endymion:0`

3. Rebuild kernel

### Main file system (F2FS)

I use [F2FS](https://wiki.archlinux.org/index.php/F2FS)

```bash
$ mkfs.f2fs -l mylabel /dev/sdxY
```

### Boot manager (GRUB)

I use [GRUB](https://wiki.archlinux.org/index.php/GRUB)

1. USB Stick must boot in UEFI mode

2. Install GRUB packages

```bash
$ pacman -S grub efibootmgr
```

3. Add Windows Support

```bash
$ pacman -S os-prober ntfs-3g
```

4. Install GRUB

```bash
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
$ grub-mkconfig -o /boot/grub/grub.cfg
```

5. Disable logo

    In file **/etc/default/grub** remove 'quiet' and 'splash'
    from GRUB_CMDLINE_LINUX_DEFAULT parameter

### User

1. Create user

```bash
$ useradd -m -G wheel -s /bin/zsh user
```

2. Set user password

```bash
$ passwd user
```

3. Allow wheel access to sudo

```bash
$ echo "%wheel ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/wheel_nopasswd \
&& chmod 400 /etc/sudoers.d/wheel_nopasswd
```

### Network (NetworkManager)

I use [NetworkManager](https://wiki.archlinux.org/index.php/NetworkManager)

```bash
$ pacman -S networkmanager
$ systemctl enable --now NetworkManager
```
