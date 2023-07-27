### Managing the Linux Boot Process

#### Can you walk us through what happens after we push the power button on our computer?

---

![[Pasted image 20220619015510.png]]

- Boot Process
  1.  BIOS/UEFI
  2.  MBR/GPT
  3.  GRUB 2
  4.  initrd/Kernel
  5.  systemd

#### Let's start at the beginning. What role does the BIOS play in booting Linux?

---

- System Firmware
  - Basic Input/Output System (BIOS)
  - Unified Extensible Firmware Interface (UEFI)
- Firmware Responsibilities
  - Initialize hardware
  - Execute boot loader

#### How does the BIOS find the boot loader?

---

- Configuration options
  - Boot order
- MBR
  - Boot data is stored in the first sector
- GPT
  - Multiple copies of the boot data are maintained

#### What does the boot data contain?

---

- **GR**and **U**nified **B**ootloader (GRUB)
  - GRUB 2
  - Open source boot loader
- Features
  - Multiple architectures
  - Graphical menus
  - Rescue mode
  - Modules
- Menu entries
  - Point to operating systems on disk
  - Point to kernels

#### Does GRUB automatically find our operating systems or do we have to configure it?

---

- Autoconfiguration
  - Performed when installing Linux
  - Can setup dual-boot configurations
  - Does not run again
- Manual configuration
  - Required any time a new OS is added
  - Required any time the kernel is updated
    - Usually handled by the kernel update package

#### Where can we find the GRUB config files?

---

- GRUB Configuration
  - `/boot/efi/EFI/centos/grub.conf`
  - Should not be edited directly
- Adding an OS to GRUB
  1.  ![[Pasted image 20220620002437.png]]
  2.  `vim /etc/grub.d/40_custom`
  3.  `grub2-mkconfig`
  4.  `cat /boot/efi/EFI/centos/grub.conf`
- Modifying GRUB Parameters (e.g. timeout)
  1.  `vim /etc/default/grub`
  2.  `grub2-mkconfig`

#### So once GRUB finds the operating system, what happens next?

---

1. Kernel is loaded
   - Loaded from `/boot/vmlinuz-<version>`
   - Compressed with gzip
   - Decompressed and loaded into RAM
2. initrd or initramfs is loaded
   - Initialization RAM disk
   - Contains a basic root (/) file system
   - Loaded from:
     - `/boot/initramfs-<version>`
     - `/boot/initrd-<version>`
3. Kernel launches SysVinit or systemd
