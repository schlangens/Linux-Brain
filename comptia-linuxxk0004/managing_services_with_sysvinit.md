### Managing Services with SysVinit

#### How are services controlled under Linux?

---

- SysVinit
  - Series of scripts that run at boot time
  - Runlevel determines the scripts
  - Upstart was a short-lived upgrade to SysVinit
- systemd
  - Replaces old init system
  - Improvements
    - Runs tasks in parallel
    - Uses cgroups to track and isolate processes
    - Provides better support for hot-plug hardware

#### How do we know if we are using SysVinit

---

- Almost all modern distros use systemd
  - Exceptions
    - Slackware
  - Process ID #1
    - `ps aux`
    - `init`
    - `systemd`
  - `ls -l /sbin/init`

#### So SysVinit starts right after the kernel, and then what happens?

---

1. BIOS/UEFI Initializes the system and locates a bootloader
2. Bootloader (usually GRUB) is initiated
   - Reads `/boot` to find the kernel
3. The Kernel is loaded
4. The Kernel executes `/sbin/init`
5. SysVinit runs the `/etc/rc.d/rc.sysinit` script

#### Does that one script then call other scripts?

---

- Runlevels:
  - 0 - Halt
  - 1 - Single user mode
  - 2 - Multiuser text mode without networking
  - 3 - Multiuser text mode
  - 4 - Unused
  - 5 - Multiuser with GUI
  - 6 - Reboot
  - NOTE: Can vary between distros
- Each runlevel maintains it's own set of scripts/configuration files
- `/etc/rc.d/rc#.d`
  - May just contain symlinks to `/etc/init.d/`
- On some older systems `/etc/rc.local` when init finishes

#### Do we have to modify the script files for each runlevel when we install a service?

---

- Set services to start at boot
  - `chkconfig httpd <on|off>`
  - `chkconfig --level 235 mysqld on`
  - `chkconfig --list`
- Manually start a service
  - `service httpd start`
  - `service httpd stop`
  - `service httpd restart`
  - `service httpd status`

#### How does SysVinit know which runlevel to boot to?

---

- Set the default runlevel in `/etc/inittab`
- Changing the run level:
  1.  Gather some information:
      - `who` (See who is logged in)
        \_ `who -r` (See the current runlevel)
  2.  Run `init #` or
  3.  Run `telinit # -t 60` (Delay 60 seconds before changing the runlevel)
  - NOTE: the time setting for telinit is unsupported on many systems, making telinit and init effectively the same.
