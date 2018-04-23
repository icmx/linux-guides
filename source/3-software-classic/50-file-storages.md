# File Storages

> **Note**
>
> Commands described in this section normally works for root user only by security and safety reasons.

### Create Filesystem — *mkfs.type*

```
mkfs.type [options...] target
```

Creates a specified *type* file system on *target* device.

Options for `extX` types (`X` may be `2`, `3` or `4`):

  - `-L` set the volume label for the filesystem
  - `-c` check for bad blocks before creating the file system

Options for `vfat` *type*:

  - `-F` FAT size (`12`, `16` or `32`)
  - `-n` volume label (up to 11 characters)

Options for `ntfs` *type*:

  - `-L` set the volume label for the filesystem
  - `-f` fast format, skipping zeroing and bad sector checking
  - `-C` enable compression on the volume

EXT4 is a common file for modern Linux systems. VFAT (i.e. FAT32) is universal, but works only with files less that 4 GBs. NTFS is a common for modern Microsoft® Windows® systems.

### *mount*

```
mount [options...] device directory
```

Mounts physical *device* or its partition to access its contents from system *directory*.

Option `-o`: comma-separated mounting options:

  - `remount`: remount system (in case it was already mounted)
  - `rw` mount in full read-write mode
  - `ro` mount in read-only mode

Example: `mount /dev/sdb2 -o ro,remount /media/user/my-flash-drive`

### *umount*

> **Note**
>
> There is no mistake, it's `umount`, not `unmount`.

```
umount target
```

Unmounts *target* which may be both device or where its directory is mounted to.

Example: `umount /media/user/my-flash-drive`

