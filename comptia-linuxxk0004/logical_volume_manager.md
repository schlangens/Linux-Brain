### Logical Volume Manager (LVM)

#### What do we need to do to get our system ready for the LVM?

---

![[Pasted image 20220616221148.png]]

- Create primary partitions on physical disks
  - `fdisk /dev/sdb`
  - n - Create new partition
  - p - primary partition
    - When done press "p" for a list
  - w - write the changes
- Install LVM tools
  - `yum install lvm2`

#### Now that we are prepared, how to we create logical volumes?

---

- Create physical volumes
  - `pvcreate /dev/sdb1 /dev/sdc1`
- Verify creation
  - `pvdisplay` or `pvs`
- Create a volume group
  - `vgcreate vg1 /dev/sdb1 /dev/sdc1`
  - `vgdisplay` or `vgs`
- Create logical volumes
  - `lvcreate -L <size> vg1 -n <name>`
  - `lvcreate -L 70G vg1 -n lv1`
  - `lvdisplay` or `lvs`

#### Are we able to format and mount the logical volumes like regular disks?

---

- Format and mount the logical volume
  - `mkfs.ext4 /dev/vg1/lv1`
  - `mount /dev/vg1/lv1 <path>`

#### Are they persistent, or do we need to add them to the file system table?

---

- Verify volume added to /etc/fstab if needed at boot
  - `more /etc/fstab/dev/mapper/vg1-lv1`
  - `/root/Videos ext4 defaults 1 1`
    - 1 - Do backup with `dump`
      - 1 - Do check for errors

#### How would we go about

---

- Add more storage to the volume group / logical volume
  - `fdisk /dev/sdd`
    - n - create new partition
    - w - write changes
  - `partprobe`
  - `pvcreate /dev/sdd1`
  - `vgextend vg1 /dev/sdd1`
  - `lvresize -L +1G /dev/vg1/lv1`
  - `df -h`
  - `resize2fs /dev/vg1/lv1`
  - `df -h`
  - `lvdisplay`

#### Is it difficult to remove the LVM if we no longer need it?

---

- Tear it all down
  - `umount <path>`
  - `lvremove /dev/vg1/lv1`
  - `vgremove /dev/vg1`
  - `pvremove /dev/sdb1 /dev/sdc1 /dev/sdd1`
