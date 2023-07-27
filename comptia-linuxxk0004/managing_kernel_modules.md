### Managing Kernel Modules

#### What are some of the things the kernel is responsible for?

---

![[Pasted image 20220619012726.png]]

- The kernel manages:
  - Memory
  - Processes
  - Devices
  - Resource allocation
  - File system access

#### So pretty much everything has to run through it?

---

![[Pasted image 20220619013014.png]]

- Kernel execution
  - User space
  - Kernel space

#### Are there different kinds of kernels available?

---

- Monolithic kernels
  - All system modules run in kernel space
  - Fast interaction between kernel and module
  - Large size (RAM)
- Microkernel
  - Most system modules run in user space
  - Smaller size
  - Worse performance
- Linux is monolithic

#### How can we see information about our kernel

---

- `uname -a`

#### Do we ever have to modify the kernel?

---

- System updates
- Load kernel modules
  - `*.ko` files
  - `/lib/modules`
  - `/usr/lib/modules`

#### How do we view and install modules?

---

- `lsmod`
  - Lists modules
  - `lsmod | less`
  - `lsmod | grep bluetooth`
- `modinfo`
  - Provides information on a module
  - `cd /lib/modules/<version>/kernel/drivers/bluetooth`
  - `modinfo btusb.ko.xz | less`
- `insmod`
  - Installs a module
- `rmmod`
  - Removes a module

#### Once a module is installed, how do we activate it?

---

- `modprobe`
  - Adds/Removes modules from the kernel
  - `/etc/modprobe.conf`
  - `/etc/modprobe.d/`
- `depmod`
  - Identifies module dependencies
- Example
  1.  `cd /etc/modprobe.d`
  2.  `sudo vim btusb.conf`
      - `alias blue btusb`
  3.  `sudo modprobe -a blue`
  4.  `lsmod | grep btusb`

#### Is there anything else we may need to configure for our kernel?

---

- Kernel options
  - Modifies the behavior of the kernel
  - `sysctl -a`
    - Lists parameters
