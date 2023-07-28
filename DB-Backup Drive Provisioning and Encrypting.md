

## Create Partition

****/dev/sde is JUST an example. The actual drive might be something else****


```

**

parted /dev/sde1

  

[root@backup-server /dev/mapper]# parted /dev/sde

GNU Parted 3.1

Using /dev/sde

Welcome to GNU Parted! Type 'help' to view a list of commands.

(parted) p

Model: Seagate Expansion Desk (scsi)

Disk /dev/sde: 4001GB

Sector size (logical/physical): 512B/4096B

Partition Table: gpt

Disk Flags:

  

Number  Start   End     Size    File system  Name                          Flags

 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres

 2      135MB   4001GB  4001GB  ntfs         Basic data partition

**




(parted) mklabel

New disk label type? gpt

Warning: The existing disk label on /dev/sde will be destroyed and all data on this disk will be lost. Do you want to continue?

Yes/No? yes

  

(parted) mkpart

Partition name?  []? db-backup-outer

File system type?  [ext2]? ext4

Start? 0%

End? 100%

(parted) p

Model: Seagate Expansion Desk (scsi)

Disk /dev/sde: 4001GB

Sector size (logical/physical): 512B/4096B

Partition Table: gpt

Disk Flags:


 ```  

``(parted) quit``





# Make the filesystem and the outer image file

  
``root@backup-server /dev/mapper]# mkfs.ext4 -L db-backup-outer /dev/sde1``

  
``tune2fs -O ^has_journal /dev/sde1``

  
(This has already been done, no need to do it again) 
``mkdir /mnt/db-backup-outer``

``mount /dev/sde1 /mnt/db-backup-outer``

``[root@backup-server /mnt/db-backup-outer]# fallocate -l 4000G image.vol``
	fallocate: fallocate failed: No space left on device



# Encrypt image.vol

NOTE: Even if drive is not 4TB it uses the same key

``cryptsetup luksFormat /mnt/db-backup-outer/image.vol db-backup --key-file /usr/local/etc/key-4T``

``cryptsetup luksOpen  /mnt/db-backup-outer/image.vol db-backup --key-file /usr/local/etc/key-4T``

 
opens as ``/dev/mapper/db-backup``


# Create Filesystem for Inner

  ``mkfs.ext4 -L db-backup /dev/mapper/db-backup``
 
At this point running 

 ``/usr/local/bin/db-backupdrive-out.ext4``
will unmount everything and

``/usr/local/bin/db-backupdrive-in.ext4``
should mount everything.


# Backup Drive Setup 

- ``parted /dev/sdX``
- . ``mklabel gpt``
- . ``mkpart``
- . ``backup``
- . ``ext4``
- . ``0%``
- . ``100%``
-  ``quit``

-  If there isn’t a key made for the backup already, /usr/local/etc/backup-key then generate one
    ``dd if=/dev/urandom of=/usr/local/etc/backup-key bs=512 count=4 iflag=fullblock``
  
   
-  ``cryptsetup luksFormat /dev/sdX1 --key-file /usr/local/etc/backup-key``
    
-  ``cryptsetup luksOpen /dev/sdX1 backup --key-file /usr/local/etc/backup-key``
    
-  ``mkfs.ext4 -L backup /dev/mapper/backup``
    
- ``ls -ls /dev/disk/by-partlabel/`` should show the drive with the label “backup”
    
-  ``ls -ls /dev/disk/by-partlabel/ | grep backup| cut -d " " -f 13|cut -d "/" -f 3`` , show the drive letter and number for the mount
    
- . Backup the key**