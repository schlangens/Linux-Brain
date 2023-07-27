## Storage

#### File System Hierarchy

## RTFM

`man hier`

### Objectives:

At the end of this episode, I will be able to:

1. Define the core components of the Linux Filesystem Heirarchy Standard.
2. Identify differences between the FHS and the implementation by Red Hat.

Red Hat Enterprise Linux uses the *Filesystem Hierarchy Standard* (_FHS_) file system structure, which defines the names, locations, and permissions for many file types and directories.

The FHS document is the authoritative reference to any FHS-compliant file system, but the standard leaves many areas undefined or extensible. This section is an overview of the standard and a description of the parts of the file system not covered by the standard.

The two most important elements of FHS compliance are:

- Compatibility with other FHS-compliant systems
- The ability to mount a `/usr/` partition as read-only. This is especially crucial, since `/usr/` contains common executables and should not be changed by users. In addition, since `/usr/` is mounted as read-only, it should be mountable from the CD-ROM drive or from another machine via a read-only NFS mount.

### Folders to be familiar with

`/boot `-  contains static files required to boot the system

The `/dev/` directory contains device nodes that represent the following device types:

![[Pasted image 20220611184519.png]]

- devices attached to the system
- virtual devices provided by the kernel.

These device nodes are essential for the system to function properly. The `udevd` daemon creates and removes device nodes in `/dev/` as needed.

Devices in the `/dev/` directory and subdirectories are defined as either *character* (providing only a serial stream of input and output, for example, mouse or keyboard) or *block* (accessible randomly, for example, a hard drive or a floppy drive). If GNOME or KDE is installed, some storage devices are automatically detected when connected (such as with a USB) or inserted (such as a CD or DVD drive), and a pop-up window displaying the contents appears.

`/bin` - Place where Binary files go (used by sys)
`/sbin` - Place where Binary file go (used by user)
`/usr` - Inside dir are another set of `/bin` & `/sbin` used by just the OS

The `/opt/` directory is normally reserved for software and add-on packages that are not part of the default installation. A package that installs to `/opt/` creates a directory bearing its name, for example `/opt/_packagename_/`. In most cases, such packages follow a predictable subdirectory structure; most store their binaries in `/opt/_packagename_/bin/` and their `man` pages in `/opt/_packagename_/man/`.

`/usr/opt` - This is where optional programs would be installed from a 3rd part vendor. This is not enforced though.

The `/media/` directory contains subdirectories used as mount points for removable media, such as USB storage media, DVDs, and CD-ROMs.

The `/mnt/` directory is reserved for temporarily mounted file systems, such as NFS file system mounts. For all removable storage media, use the `/media/` directory. Automatically detected removable media will be mounted in the `/media` directory.

The `/proc/` directory contains special files that either extract information from the kernel or send information to it. Examples of such information include system memory, CPU information, and hardware configuration.

The `/lib/` directory should only contain libraries needed to execute the binaries in `/bin/` and `/sbin/`. These shared library images are used to boot the system or execute commands within the root file system

The `/sbin/` directory stores binaries essential for booting, restoring, recovering, or repairing the system. The binaries in `/sbin/` require root privileges to use. In addition, `/sbin/` contains binaries used by the system *before* the `/usr/` directory is mounted; any system utilities used after `/usr/` is mounted are typically placed in `/usr/sbin/`.

At a minimum, the following programs should be stored in `/sbin/`:

- `arp`
- `clock`
- `halt`
- `init`
- `fsck.*`
- `grub`
- `ifconfig`
- `mingetty`
- `mkfs.*`
- `mkswap`
- `reboot`
- `route`
- `shutdown`
- `swapoff`
- `swapon`

`/home` & `/home/srv` are very similar but `/srv` are user accounts like a service used by applications

The `/srv/` directory contains site-specific data served by a Red Hat Enterprise Linux system. This directory gives users the location of data files for a particular service, such as FTP, WWW, or CVS. Data that only pertains to a specific user should go in the `/home/` directory.

**Note**

The default httpd install uses `/var/www/html` for served content.

`/var` - Temp data, where log files go. Print spooler

`/etc` - where configuration files go

### External Resources:

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/storage_administration_guide/ch-filesystem

- [Filesystem Hierarchy Standard (FHS)](http://www.pathname.com/fhs/)
- [Official Red Hat Documentation](https://access.redhat.com/articles/rhel8-abi-compatibility)
