### Filesystem Hierarchy Standard (FHS)

#### Who created the FHS?

---

- [The Linux Foundation](https://www.linuxfoundation.org/)

#### Where can we view the official standard?

---

- [Filesystem Hierarchy Standard (FHS)](http://www.pathname.com/fhs/)

#### Do all Linux distributions adhere to the FHS?

---

- Most conform, but almost all deviate in one way or another
- Typically when it comes to binaries
  - Links are often used to preserve compatibility
- [Official Red Hat Documentation](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch-filesystem.html#s1-filesystem-fhs)
  - `/sbin/` is linked to `/usr/sbin`

#### Where would we normally find applications?

---

- `/bin/`
  - Essential user command binaries
  - Available to all users
- `/sbin/`
  - System binaries
  - Required for the system to boot
- `/usr/bin/`
  - Most user commands
- `/usr/sbin/`
  - Non-essential standard system binaries
- `/opt/`
  - Contains software not included with the installation

#### What are some of the other key folders we need to be familiar with?

---

- `/boot/` - Contains boot files and the Linux kernel
- `/dev/` - Contains device nodes representing hardware
- `/etc/` - Contains configuration files
- `/mnt/` - Contains temporary mount points for media
- `/proc/` - Virtual file system containing data files for processes on the system
- `/sys/` - Virtual file system containing data for hot plug devices. Similar to `/proc/`
- `/usr/` - Contains binaries and data sharable between users
  - Mounted read-only per FHS
- `/var/` - Contains variable data for programs in `/usr/`

#### Do we really need to have all these folders memorized?

---

- For the exam, certainly
- In real-life you can cheat a bit
  - `which <command>`
  - `whereis <command>`
  - `locate`
  - `find`
