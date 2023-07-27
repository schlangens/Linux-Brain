## Storage

#### Creating Volumes with LVM

### Objectives:

At the end of this episode, I will be able to:

1. Install the LVM on a RHEL8 system.
2. Create and mount volumes using the LVM.

`lsblk`
![[Pasted image 20220611164143.png]]

- Look at your mounts
  `mount`

`sudo pvdisplay` - Physical Volume - This disc allowed to be used by LVM
`pvcreate /dev/<device> - From lsblk- nvme0n2`
![[Pasted image 20220611164857.png]]
`y`
`pvs - Shorter command for pvdisplay - physical volume show`
`sudo vgdisplay` - Volume Group
`vgcreate vg1 /dev/nvme0n2 /dev/nvme0n3`
![[Pasted image 20220611165208.png]]
`vgdisplay`
![[Pasted image 20220611165345.png]]
`sudo lvdisplay` - Logical Volumes -
`lvcreate -L 250G vg1 -n website`
`lvdisplay`
![[Pasted image 20220611165600.png]]
`vgdisplay`
![[Pasted image 20220611170101.png]]

### Format and Mount (to /website)

`mkdir /website`
`mkfs.xfs /dev/vg1/website`
![[Pasted image 20220611170311.png]]
`mount /dev/vg1/website /website`
`df -h`
![[Pasted image 20220611170423.png]]

### To make perm edit the fs table file

`sudedit /etc/fstab`

```config

/dev/mapper/vg1-website /website  xfs defaults 1 1


```

### Install LVM - Installed by default with RHEL8

`sudo dnf install lvm2`

- Say you have 3 disc on the system w/ nothing on them you can use them with LVM once you create 1 partition on them with the following:
  - `sudo -s` - get into root shell
  - `fdisk /dev/nvme0n2`
  - ![[Pasted image 20220611164316.png]]
  - `n`
  - `p`
  - `enter`
  - `w`
  - DO THIS ON ALL OTHER DISK from `lsblk`
