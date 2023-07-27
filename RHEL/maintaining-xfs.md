## Storage

#### Maintaining XFS

### Objectives:

At the end of this episode, I will be able to:

1. Format and mount a disk with XFS.
2. Assign and modify volume labels for proper mounting of XFS volumes.
3. Repair common file system errors on XFS volumes.

## Maint task

#### Make XFS FS

`sudo mkfs.xfs /dev/<device name from lsblk>`
`sudo mount /dev/nvme0n2p1 /website`

#### Increase Size

`sudo fdisk /dev/<drive>`
`p`
![[Pasted image 20220611183134.png]]

`sudo xfs_grow /website -D 20`

### What do we do if we see FS errors? Flushing the Journal

`sudo umount /website`
`sudo mount /dev/nvme0n2p1 /website`

- When you unmount it gets rid of all partial writes and recovers the the original full file
  Prevents writing new data to the bad sector of the drive - replace the rdirve
  `umount /website`
  `sudo xfs_repair /dev/nvme0n2`

`sudo xfs_admin -l /dev/nvme0n2`
![[Pasted image 20220611191210.png]]
`sudo xfs_admin -L "website" /dev/nvme0n2`

## Retrieve UUID of drive

`sudo xfs_admin -u /dev/nvme0n2`
![[Pasted image 20220611191445.png]]

`sudoedit /etc/fstab`
![[Pasted image 20220611191734.png]]

- This UUID will never change -> It will always be correct
