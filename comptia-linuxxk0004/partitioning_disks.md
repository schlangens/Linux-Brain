### Partitioning Disks

#### What partition types are supported in Linux?

---

- Partitioning Types
  - MBR Partitions
    - Primary Partitions
    - Extended Partitions
    - Logical Partitions
  - GPT Partitions
    - Does away with primary/extended/logical
    - 128 definable partitions by default

#### What commands do we use to modify our partitions?

---

- Using `fdisk` for MBR disks
  - `sudo fdisk -l /dev/sdb`
  - `sudo fdisk /dev/sdb`
  - `p` prints the file table
  - `n` creates a new partition
  - `w` writes changes
  - Sizes can be entered (+0M, -3000M, etc)
- Using `gdisk` for GPT disks
  - `sudo gdisk /dev/sdc`
  - `p` prints the file table
  - `n` creates a new partition
  - `w` writes changes

#### Are there any tools that do both MBR and GPT?

---

- Using `parted` for MBR, GPT, APM, and BSD
  - `sudo parted /dev/sdb`
  - `print`
  - `mkpart`

#### What if I am a GUI junkie? Are there graphical tools we could use?

---

- GUI `Disks` partition software
  - Part of GNOME
  - `Applications -> Utilities -> Disks`
