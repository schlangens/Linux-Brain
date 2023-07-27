### Linux File Systems

#### How do we choose which file system to use?

---

- EXT[2,3,4]
  - Extended Filesystem
  - EXT3 is the most common Linux file system
    - Stable and well supported
    - Uses bitmapping which can be inefficient
  - EXT4 is an update to EXT3
    - Increases file and volume sizes
    - Uses extents instead of bitmapping
    - Incorporates journaling
- XFS
  - Extents Filesystem
  - Successor to EXT
  - Default file system as of RHEL7
  - Increases supported file system sizes
  - Incorporates journaling
  - File system can grow, but cannot shrink
- BTRFS
  - B-Tree Filesystem
  - Currently in preview
  - Massive file system sizes
  - Incorporates journaling and a number of other features
    - Integrated LVM
  - Not supported in RHEL

####

---

- Creating a filesystem
  - Numerous utilities
    - Look in `ls -la /usr/sbin/mk*`
    - `mkfs` and its subordinates are just wrappers
      for utilities like `mke2fs`
  - Examples
    - `sudo mkfs -t ext3 /dev/sdb1`
    - `sudo mkfs -t ext4 /dev/sdb1`
    - `sudo mkfs.ext3 /dev/sdb1`
    - `sudo mkfs.ext4 /dev/sdb1`
  - Creating swap space
    - `sudo mkswap /dev/sdb2`
    - `sudo swapon /dev/sdb2`

#### Can we change a file system after it is created?

---

- Labels
  - `e2label /dev/sdb1 Storage`
  - `xfs_admin -L Storage /dev/sdb1`
- Resizing filesystems
  - Possible using utilities like `resize4fs` or LVM

#### How do we start using the new file system?

---

- Mounting Partitions
  - `mount [-alrsvw] [-t fstype] [-o options] [device] [mountpoint]`
  - `mount -a`: Mount all filesystems in `/etc/fstab`
  - `mount -r`: Mount as _read only_
  - `mount -w`: Mount as read/write
  - `mount -t`: Specify the filesystem type
  - `mount -o`: Specify additional options
  - `[device]`: Specify the device filename that is to be mounted - `/dev/fd0` - `/dev/cdrom` - `/dev/hda4`
  - `[mountpoint]`: Specify the directory to which the device's contents should be attached
  - `sudo mount /dev/sdb1 /home/dpezet/Files`
- Unmounting Partitions
  - `sudo umount /dev/sdb1 /home/dpezet/Files`

#### Will the file systems still be mounted if we reboot?

---

- Make mounting changes permanent by editing the `/etc/fstab` file
  - `[Device] [Mount Point] [File System Type] [Options] [Dump] [Pass]`
  - `Dump` is normally `0`
    - Set to `1` if you use the `dump` utility to backup disks
  - `Pass` determines the order `fsck` checks the disks
    - `1` for root
    - `2` for everything else

#### How do we pick where to mount a file system?

---

- Mount Points
- Common Partitions and File System layouts
  - Swap
  - `/home`
  - `/boot`
  - `/usr`
  - `/usr/local`
  - `/opt`
  - `/var`
  - `/tmp`
  - `/mnt`
  - `/media`
