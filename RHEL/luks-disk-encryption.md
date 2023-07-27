## Security

#### LUKS Disk Encryption

### Objectives:

At the end of this episode, I will be able to:

1. Describe the basic operations of LUKS disk encryption.
2. Use shred to securely erase a disk.
3. Use cryptsetup to encrypt and mount a volume from the CLI.
4. Configure RHEL to automatically mount encrypted volumes at boot.
5. Configure additional security keys to decrypt a LUKS volume.

`lsblk`

- To encrypt drive - Make sure you have backup, process disk, encrypt, put data back on.. Like so

` `sudo -s` `umount /website``

### New disc pickup

`shred -v --iterations=1 /dev/nvm0n3p1`
![[Pasted image 20220613001759.png]]

`lsblk`
![[Pasted image 20220613001912.png]]

`sudo blkid /dev/nvme0n1p2`
![[Pasted image 20220613002027.png]]

### Before encryption on nvme9n2p1

``blkid <device>
![[Pasted image 20220613002211.png]]

`cryptsetup --verbose --verify-passphrase luksFormat /dev/nvme02np1`
`Y`
`PASSPHRASE`
![[Pasted image 20220613002350.png]]

## Verify your work

`blkid /dev/nvme02np1`
![[Pasted image 20220613002513.png]]

## Open the encrypted drive

`cryptsetup luksOpen /dev/nvme02np1 website`
`PASSPHRASE`

Now `lsblk`
![[Pasted image 20220613002655.png]]

## Now that its open - put a FS on it

`mkfs.xfs /dev/mapper/website`

- Remember when we look at the blkid it will show xfs
- `blkid`
- ![[Pasted image 20220613002911.png]]

- To make perm we need to add to `/etc/cryptab`
- It will also show use encrypted volumes unlocked
- ![[Pasted image 20220613003201.png]]

`sudoedit /etc/crypttab`

```config
website /dev/nvme0n2p1 <password>
```

- Its okay to do this because the Root Volume is encrypted and requires a password at boot

`sudoedit /etc/fstab`

```config

 /dev/mapper/website /website xfs defaults 1 1


```

### Restore the files

`sudo cp /path/to/backup/* ./`

- Now those files are encrypted !!!

### Maint tasks

`cryptsetup luksAddKey /dev/nvme0n2p1`
`cryptsetup luksRemoveKey /dev/nvme0n2p1`
![[Pasted image 20220613003902.png]]
