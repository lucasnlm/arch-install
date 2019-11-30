### Partitioning without Cryptography

Run the following commands:

```bash
fdisk -l
cfdisk /dev/nvme0n1
```

If your hardware supports UEFI, select `gpt`. Otherwise select `dos`.

Create the following partitions:

| Partition | Location       | Size | Type             |
| --------- | -------------- | ---- | ---------------- |
| Boot      | /dev/nvme0n1p1 | 512M | EFI System       |
| /         | /dev/nvme0n1p2 | 25G  | Linux Filesystem |
| /home     | /dev/nvme0n1p3 | \*   | Linux Filesystem |

Check if the partitions were created:

```bash
fdisk -l /dev/nvme0n1
```

If your storage device is SATA, it will be `sda` instead of `nvme0n1`.

### Formatting and making the filesystems

Run the following commands to format the partitions:

```bash
mkfs.vfat -F32 -n EFI /dev/nvme0n1p1
mkfs.ext4 /dev/nvme0n1p2
mkfs.ext4 /dev/nvme0n1p3
```

And then mount them:

```bash
mount /dev/nvme0n1p2 /mnt
mkdir -p /mnt/boot/EFI
mount /dev/nvme0n1p1 /mnt/boot
mkdir /mnt/home
mount /dev/nvme0n1p3 /mnt/home
ls /mnt
```

Check if they are correctly mounted using:

```bash
findmnt
```
