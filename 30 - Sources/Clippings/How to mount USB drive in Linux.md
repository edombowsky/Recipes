---
title: "How to mount USB drive in Linux"
source: "https://linuxconfig.org/howto-mount-usb-drive-in-linux"
author:
  - "Lubos Rendek"
published: 2024-04-02
created: 2025.12.22 00:00:00.000-08:00
description: "Learn how to mount USB drives on Linux using the command line. This guide covers detection, mounting, and troubleshooting USB drives."
tags: ["clippings"]
updated: 2025.12.22 19:49:47.059-08:00
---
Mounting USB drive is no different than mounting USB stick or even a regular SATA drive. The video example below will illustrate the entire process of mounting USB drive on Linux system. To gain more understanding, read the subsequent paragraphs. In Linux, you can mount all file systems including ext4, FAT, and NTFS.

In this tutorial, we explain how to mount USB drives in a [Linux system](https://linuxconfig.org/linux-download) using terminal and shell command line. This allows you to mount a USB drive of any file system, to some mount point on your system. If you are using desktop manager, you will most likely be able to use it to mount USB drive for you.

**In this tutorial you will learn how to:**

- Detect your USB drive
- Create a custom mount point
- Mount USB in Linux
- Access USB drive’s data  
![mount usb linux](https://linuxconfig.org/wp-content/uploads/2013/03/00-howto-mount-usb-drive-in-linux.avif)

How to mount USB drive in Linux

## Software Requirements and Conventions Used

| Category    | Requirements, Conventions, or Software Version Used                                                                                                                                                                                                                                                               |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| System      | Any GNU/Linux Distribution                                                                                                                                                                                                                                                                                        |
| Software    | mount, fdisk                                                                                                                                                                                                                                                                                                      |
| Other       | Privileged access to your Linux system as root or via the `sudo` command.                                                                                                                                                                                                                                         |
| Conventions | **#** – requires given [linux commands](https://linuxconfig.org/linux-commands) to be executed with root privileges either directly as a root user or by use of `sudo` command<br>**$** – requires given [linux commands](https://linuxconfig.org/linux-commands) to be executed as a regular non-privileged user |

## Video Example on how to Mount USB in Linux

![YouTube video](https://i.ytimg.com/vi/-tDquvejreE/hqdefault.jpg)

1. ## Detecting USB hard drive
	After you plug in your USB device to the USB port, Linux system adds a new block device into `/dev/` directory. At this stage, you are not able to use this device as the USB [filesystem](https://linuxconfig.org/filesystem-basics) needs to be mounted before you can retrieve or store any data. To find out what name your block device file have you can run `fdisk -l` [command](https://linuxconfig.org/linux-commands).

>[!note]  
>`fdisk` command requires administrative privileges to access the required information, thus, from this reason, the commands needs to be executed as a root user or with `sudo` prefix.

```shell
	\# fdisk -l 
	OR
	$ sudo fdisk -l
```

Upon executing the above command you will get an output similar to the one below:

```plaintext
Disk /dev/sdc: 7.4 GiB, 7948206080 bytes, 15523840 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000
Device     Boot Start      End  Sectors  Size Id Type
/dev/sdc1  *     8192 15523839 15515648  7.4G  b W95 FAT32
```

The above output will most likely list multiple disks attached to your system. Look for your USB drive based on its size and filesystem. Once ready, take a note of the block device name of the partition you intent to mount. For example in our case that will be `/dev/sdc1` with FAT32 filesystem.  
2. ## Create mount point  
	Before we are able to use **mount** command to mount the USB partition, we need to create a mount point. Mount point can be any new or existing directory within your host filesystem. Use `mkdir` command to create a new mount point directory where you want to mount your USB device:  
	```

# Mkdir /media/usb-drive

	```
3. ## Mount USB Drive  
	At this stage we are ready to mount our USB’s partition `/dev/sdc1` into `/media/usb-drive` mount point:  
	```

# Mount /dev/sdc1 /media/usb-drive/

	```
	To check whether your USB drive has been mounted correctly execute [**mount** command](https://linuxconfig.org/mount) again without any arguments and use `grep` to search for USB block device name:
	```

# Mount | Grep Sdc1

	/dev/sdc1 on /media/usb-drive type vfat (rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=utf8,shortname=mixed,errors=remount-ro
	```
	If no output has been produced by the above **mount** command your USB partition is not mounted. Alternatively, double-check whether you have used a correct block device name in the above command.
4. ## Accessing USB Data  
	If all went well, we can access our USB data simply by navigating to our previously created mount point `/media/usb-drive`:  
	```

# Cd /media/usb-drive

	```

---

---

## USB Unmount

Before we are able to unmount our USB partition we need to make sure that no process is using or accessing our mount point directory, otherwise we will receive an error message similar to the one below:

```plaintext
umount: /media/usb-drive: target is busy
(In some cases useful info about processes that
use the device is found by lsof(8) or fuser(1).)
```

Close your shell or navigate away from USB mount point and execute the following [linux command](https://linuxconfig.org/linux-commands) to unmount your USB drive:

```plaintext
# umount /media/usb-drive
```

## Permanent USB Mount in Linux

In order to mount your USB in Linux permanently after reboot add the following line into your `/etc/fstab` config file:

```plaintext
/dev/sdc1       /media/usb-drive           vfat    defaults        0       0
```

For any other file system type simply set correct type. For example the bellow command will mount USB driver with NTFS file system:

```plaintext
/dev/sdc1       /media/usb-drive           ntfs    defaults        0       0
```

From this reason it is recommend to use partition `UUID` instead of a raw block device name. To do so, first [locate a UUID of your USB drive](https://linuxconfig.org/how-to-retrieve-and-change-partitions-universally-unique-identifier-uuid-on-linux):

```plaintext
# ls -l /dev/disk/by-uuid/*
lrwxrwxrwx 1 root root 10 Mar 27 23:38 /dev/disk/by-uuid/2016-08-30-11-31-31-00 -> ../../sdb1
lrwxrwxrwx 1 root root 10 Mar 27 23:38 /dev/disk/by-uuid/3eccfd4e-bd8b-4b5f-9fd8-4414a32ac289 -> ../../sda1
lrwxrwxrwx 1 root root 10 Mar 27 23:38 /dev/disk/by-uuid/4082248b-809d-4e63-93d2-56b5f13c875f -> ../../sda5
lrwxrwxrwx 1 root root 10 Mar 28 01:09 /dev/disk/by-uuid/8765-4321 -> ../../sdc1
lrwxrwxrwx 1 root root 10 Mar 27 23:38 /dev/disk/by-uuid/E6E3-F2A2 -> ../../sdb2
```

Based on the above `ls` command output we can see that the UUID belonging to block device `sdc1` is `8765-4321` thus our `/etc/fstab` mount line will be:

```plaintext
/dev/disk/by-uuid/8765-4321    /media/usb-drive         vfat    defaults   0   0
```

Run `mount -a` command to mount all not yet mounted devices.

```plaintext
# mount -a
```

## Closing Thoughts

In this tutorial, we saw how to mount a USB drive on a Linux system in order to access its data and store new data onto it. Linux makes it possible to either temporarily mount a USB drive that we insert, or make a persistent mount of storage devices that we don’t plan on removing. Whether you have a small thumb drive or a huge external drive, the commands here should be able to mount your USB storage device.

## Troubleshooting Common USB Mount Error Messages on Linux

- ### No Medium Found
	You may receive the following error when you attempt to mount a USB stick:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: no medium found on /dev/sdx.
	```

	**Solution:**  
	Ensure that the USB drive is properly connected and that you are using the correct device file. Sometimes, reconnecting the USB drive or using a different USB port can resolve the issue.
- ### NTFS Filesystem Unsupported
	When attempting to mount an NTFS USB drive, you may encounter this error:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: unknown filesystem type 'ntfs'.
	```

	**Solution:**  
	Install the [ntfs-3g](https://linuxconfig.org/how-to-install-ntfs-3g-on-redhat-8) package to add support for NTFS file systems on your Linux system. You can [install ntfs-3g](https://linuxconfig.org/how-to-install-ntfs-3g-on-redhat-8) using your package manager to install it, for example, sudo apt-get install ntfs-3g.
- ### Generic Mount Error
	A generic error that can occur for various reasons:  
	**Error message:**

	```plaintext
	mount: wrong fs type, bad option, bad superblock on /dev/sdx1, missing codepage or helper program, or other error.
	```

	**Solution:**  
	Verify the file system type and ensure you have the necessary support installed. For file system errors, use tools like `fsck` to check and repair your drive.
- ### Cannot Mount Read-Only
	This error occurs when attempting to mount a USB drive as read-only, but the operation fails:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: cannot mount /dev/sdx1 read-only.
	```

	**Solution:**  
	Check the drive for hardware switches enabling write protection, or use `dmesg` to look for I/O errors that may suggest hardware issues. Make sure the file system is not corrupted.
- ### Superuser Privileges Required
	Attempting to mount without sufficient permissions results in this error:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: must be superuser to use mount.
	```

	**Solution:**  
	Ensure you’re using `sudo` before your mount command to execute it with superuser privileges, e.g., `sudo mount /dev/sdx1 /mnt/usb`.
- ### Special Device Does Not Exist
	This message suggests that the specified device file does not exist:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: special device /dev/sdx1 does not exist.
	```

	**Solution:**  
	Double-check the device file name for typos. Use `lsblk` or `fdisk -l` to list available devices and verify the correct device identifier.
- ### Fstab Entry Missing
	If the system cannot find the [fstab entry](https://linuxconfig.org/how-fstab-works-introduction-to-the-etc-fstab-file-on-linux) in `/etc/fstab`, this error will occur:  
	**Error message:**

	```plaintext
	mount: /mnt/usb: can't find in /etc/fstab.
	```

	**Solution:**  
	If you wish to mount the device without specifying the device file and mount point each time, add an entry to `/etc/fstab`. Ensure that the entry matches your device and desired mount point accurately.

## FAQs on Mounting USB Drives on Linux

1\. How do I find my USB drive in Linux?

Use the command `lsblk` or `fdisk -l` to list all connected drives, including USB drives. Look for the device that corresponds to your USB drive by its size and partition type.

2\. How can I mount a USB drive manually?

Create a mount point using `mkdir /mnt/usb` and then mount the USB drive with `sudo mount /dev/sdx1 /mnt/usb`, replacing `/dev/sdx1` with your USB device identifier.

3\. How do I unmount a USB drive?

Use the command `sudo umount /mnt/usb`, ensuring no files are being accessed from the USB drive.

4\. Can I mount a USB drive automatically when it’s plugged in?

Yes, by configuring `/etc/fstab` or using a GUI tool like GNOME Disks to set up automount options.

5\. How do I check if my USB drive is mounted?

Use `df -h` or `lsblk` to see if your USB device is listed as mounted.

6\. Why can’t I write to my USB drive after mounting it?

This could be due to the drive being mounted as read-only. Try remounting with write permissions using `sudo mount -o remount,rw /mnt/usb`.

7\. How do I mount a USB drive with a specific filesystem type?

Use the `-t` option with `mount`, like `sudo mount -t vfat /dev/sdx1 /mnt/usb` for a FAT32 filesystem.

8\. What does “mount point” mean?

A mount point is a directory in the Unix filesystem where the USB drive’s contents will be accessible after it is mounted.

9\. How do I create a new mount point?

Create a directory using `mkdir`, such as `mkdir /mnt/new_usb`, which then can be used as a mount point.

10\. How can I see the mount options of a mounted USB drive?

Use `mount | grep /mnt/usb` to display the mount options of the USB drive mounted at `/mnt/usb`.

11\. Can I mount multiple USB drives at the same time?

Yes, each USB drive needs to be mounted to a different mount point.

12\. How do I fix “mount: unknown filesystem type” error?

Ensure you have the correct filesystem drivers installed for your USB drive’s filesystem type. For NTFS, you might need the `ntfs-3g` package.

13\. How to mount a USB drive read-only?

Use `sudo mount -o ro /dev/sdx1 /mnt/usb` to mount the drive as read-only.

14\. What do I do if my USB drive is not recognized?

Check USB ports and try a different one. Ensure the drive is properly formatted and visible with `lsusb` and `fdisk -l`.

15\. How to auto-mount USB drives in a specific directory?

Use the UUID of the USB drive in `/etc/fstab` and specify the desired mount point, or use automount tools like udev rules for more dynamic handling.

---

---

**Comments and Discussions**  
![Linux Forum](https://linuxconfig.org/wp-content/uploads/2024/04/linuxconfig-forum-logo-1.webp)
