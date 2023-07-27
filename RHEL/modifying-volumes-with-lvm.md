## Storage

#### Modifying Volumes with LVM

### Objectives:

At the end of this episode, I will be able to:

1. Increase the storage available to a LVM volume.
2. Delete volumes that are no longer required.

### Lets add a disk to the VG

`lsblk`
![[Pasted image 20220611171553.png]]
`pvdisplay`
![[Pasted image 20220611171648.png]]
`pvcreate /dev/nvme0n4`
`y`
![[Pasted image 20220611171838.png]]
`pvs`
![[Pasted image 20220611171857.png]]

- Before we incorporate our new physical vol..
- `vgs`
- ![[Pasted image 20220611172016.png]]
- `vgextend vg1 /dev/nvme0n4`

## Increase Logical Volume

- You can use percentages
  `lvresize -L +50G /dev/vg1/website`
  ![[Pasted image 20220611172738.png]]

### How to tell what FS you have

`mount | grep website`
![[Pasted image 20220611174449.png]]

### if Ext4

`resize2fs /dev/vg1/website`

## If XFS

`xfs_growfs /website` - Only supports growing - no shriking
![[Pasted image 20220611174846.png]]

## Lets verify its done

`df -h`
![[Pasted image 20220611174944.png]]

### Tear it all down (go backwards)

`umount /website` Also remove entry at `/etc/fstab` (File System Table)
`lvremove /dev/vg1/website`
`vgremote /dev/vg1`
``pvremove /dev/nvme0n2 /dev/nvme0n2
