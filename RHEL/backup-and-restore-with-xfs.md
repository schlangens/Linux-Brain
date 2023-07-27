## Storage

#### Backup and Restore with XFS

### Objectives:

At the end of this episode, I will be able to:

1. Backup an XFS volume to tape or disk using the xfsdump command.
2. Configure a backup rotation and perform incremental backups using xfsdump.
3. Restore individual files or entire XFS volumes from backups.

## Check for xfsdump - Is it installed?

`which xfsdump`

DISCOVERY FUNCTION

### Take a look at your disk

`lsblk`

### Backup your Website we created earler with xfsdump

![[Pasted image 20220611192654.png]]

`mount`
![[Pasted image 20220611192745.png]]

![[Pasted image 20220611193110.png]]

## For larger datasets use incrementals or differentials

- Incrementals whats changes since the last backup
- `sudo xfsdump -f /home/sschlangen/website.bak -l 1 -M website -L T-Inc /website` - This would be your Tuesday Incremental `-L T-Inc`. Notice we use level on our command rather than 0 for full. Incrementals {1.9} _Maxes out at 9_. Then do another full backup - Full Backup - Then incrementals as you want per app load -`sudo xfsdump -f /home/sschlangen/website1.bak -l 0 -M website -L full_backup /website`
- Differential - backup all the way to the full backup
  `xfsdump -i`

### Restore the mofo

`sudo xfsrestore -r -f /home/website.back /website`
![[Pasted image 20220611194544.png]]

#### Example of just restoring a file. Takes a bit more effort. We will be restoring the index.html file in this example

`sudo xfsrestore -f /home/dpexet/website -L full_backup -s index.html /home/sschlangen/website`

![[Pasted image 20220611194957.png]]
