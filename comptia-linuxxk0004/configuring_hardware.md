### Configuring Hardware

#### What types of hardware do we typically work with in Linux?

---

- USB
  - Printer
  - Webcam
  - Keyboard
  - Mouse
- Wireless
  - Wi-Fi
  - Bluetooth
- PCI
  - Video
  - Network
- Storage
  - SATA
  - SCSI
  - HBA

#### Where can we find our hardware in the OS?

---

- All hardware is represented in `/dev`
  - `udev` daemon maps hardware to files in `/dev`
  - Device files are dynamic
    - Missing hardware does not show up

```
	/dev/cdrom
	/dev/cpu
	/dev/mem
	/dev/sda
	/dev/sda1
	/dev/snd
	/dev/stdout
	/dev/tty##
```

#### What if our device names differ from someone else's?

---

- Device mappings can be overridden if necessary
  - `/etc/udev/rules.d`
  - To rename eth1 to eth0
    - `vim /etc/udev/rules.d/70-persistent-net.rules`
    - Change as required

#### Do we have to do anything special to make the rules take effect?

---

- The rules load automatically, but are not applied
  - Can force a rule reload
  - `sudo udevadm control --reload-rules`
- To make the rules apply do one of the following:
  - Reboot
  - Disconnect/Reconnect device
  - `sudo udevadm trigger`

#### Are there any other ways we can verify that hardware is detected properly?

---

- List connected hardware
- Call `/sys`
  - `lspci`
  - `lsusb`
  - `lsdev`

#### What if our hardware isn't being detected?

---

- Cold plug vs Hot plug
  - Cold may require a reboot
- Check the logs to see if the hardware shows up
  - `dmesg`
  - `dmesg -w` or `dmesg --follow`
- Generate a hardware report
  - Query the device management interface
  - `dmidecode`
  - `ls /sys/bus/pci/devices`
  - `ls /sys/bus/pci/drivers/e1000`
