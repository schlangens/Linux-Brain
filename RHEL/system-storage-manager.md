## Storage

#### System Storage Manager

### Objectives:

At the end of this episode, I will be able to:

1. Install the System Storage Manager (SSM).
2. Use the SSM to create and resize volumes in LVM.
3. Use the SSM to create RAID 0 and RAID 1 storage arrays.

- This is usually not installed by default
- lets check `which ssm`
- ![[Pasted image 20220611195358.png]]

`sudo dnf install system-storage-manager`

`sudo -s`
`ssm list`
`ssm list volumes`

## Why is SSM so great?

`ssm create -s 100G -n website --fstype xfs -p vg2 /dev/nvme0n2p1 /dev/nvme0n3p1 /website`
![[Pasted image 20220611200015.png]]

`ssm resize -s +10G /dev/vg1/website /dev/nvme0n4p1`

### Check for errors w. SSM

`sudo umount /website`
``ssm check /dev/vg1`

### Tear down SSM

`sudo ssm remove vg1`

### Raid 0 Stripe for Performance

`sudo ssm create --raid 0 -n website --fstype xfs vg3 /dev/nvm0n2p2`
