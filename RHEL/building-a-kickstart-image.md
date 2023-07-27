## Introduction to RHEL

#### Building a Kickstart Image

### Objectives:

At the end of this episode, I will be able to:

1. Create a RHEL installation image using a Kickstart configuration file.
2. Manually call the configuration file at boot time.
3. Fully automate the process and have the installer load the Kickstart file by default

`system-config-kickstart`

Or use the customer portal
Step 1: https://access.redhat.com
Generate kickstart.cfg

Boot to RHEL - hit `tab`
specify kickstart at diff location like nfs fileshare

### Or bake the kickstart

rename `kickstart.cfg` to `ks.cfg`
drop to root of drive

## How to make custom install

1. get the ISO
2. mount the ISO ``sudo mount -o loop <path/to/iso> /mnt/cdrom
3. once you mount this it will be read-only
4. Copy all the contents `cd /mnt/cdrom | mkdir ~/rhel8-custom | cp -R * ~/rhel8-custom `
5. `sudo cp ~/Downloads/kickstart.cfg ./ks.cfg`

### Modify Init

`sudoedit ~/rhel8-custom/isolinux.cfg`

```config

label webserver
	menu label Install RHEL8 Web Server Kickstart
	kernel vmlinuz
	append initrd=initrd.img inst.stage2=:LABEL=RHEL-8-1-0-BaseOS-x86_64 quiet ks=nfs:10.0.0.1:/exports/kickstart/webserver.cfg

label accounting
	menu label Install RHEL8 Accounting Laptop Kickstart
	kernel vmlinuz
append initrd=initrd.img inst.stage2=:LABEL=RHEL-8-1-0-BaseOS-x86_64 quiet ks=
ks=nfs:10.0.0.1:/exports/kickstart/accounting.cfg

label admin
	menu label Install RHEL8 Admin Workstation Kickstart
	kernel vmlinuz
append initrd=initrd.img inst.stage2=:LABEL=RHEL-8-1-0-BaseOS-x86_64 quiet ks=
ks=nfs:10.0.0.1:/exports/kickstart/admin.cfg

```

Rebuild the image
`cd ~`
`sudo mkisofs -o rhel8-custom.iso -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -R -J -V rhel8-custom /home/sschlangen/rhel8-custom`

### Resources

- [Web-based Kickstart Generator](https://access.redhat.com/labs/kickstartconfig/)
-
