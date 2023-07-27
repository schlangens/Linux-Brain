### Backup and Restore Data

#### How do we decide what kind of backups we need?

---

- Backup Types
  - Full [DIAGRAM 49]
  - Differential [DIAGRAM 50]
  - Incremental

#### How are these backups stored?

---

- Physical Media
  - Tape
  - Optical
  - HDD
- Digital Storage
  - Snapshot
  - Image
  - Clone

#### What is a quick and easy way to backup files?

---

- `tar`
  - **T**ape **AR**chiver
  - Originally developed for tape
  - Can be used with almost any media
- Create an archive
  - `tar cvzf backup.tgz ~/Documents`
- Extract an archive
  - `tar xvzf backup.tgz`
  - `tar xvzf ~/Documents2/ backup.tgz`

#### Can we tell tar to only backup files that have changed?

---

- `dar`
  - **D**isk **AR**chiver
  - Replacement for `tar`
  - Supports differential and incremental backups
- Create a full backup
  - `dar -R ~/Documents -c full.bak`
- Create a differential backup
  - `dar -R ~/Documents -c full.bak`
  - `dar -R ~/Documents -c diff1.bak -A full.bak`
- Create incremental backups
  1.  `dar -R ~/Documents -c full.bak`
  2.  `dar -R ~/Documents -c incr1.bak -A full.bak`
  3.  `dar -R ~/Documents -c incr2.bak -A incr1.bak`
- Restore backups
  1.  `dar -x full.bak`
  2.  `dar -x incr1.bak -w`
  3.  `dar -x incr2.bak -w`

#### Can we backup an entire disk with dar?

---

- `dd`
  - Stands for "Copy and Convert"
    - CC was already in use
  - Can clone an entire disk
  - Allows backups of almost any file system
- Copy a disk to another disk
  - `dd if=/dev/sda of=/dev/sdb`
- Make an image of a disk
  - `dd if=/dev/sda of=drive_image.img`
- Restore an image to a disk
  - `dd if=drive_image.img of=/dev/sdb`

#### Are there any other backup technologies we should know about?

---

- Backup Utilities
  - `mirrorvg`
  - `scp`
  - `sftp`
  - `rsync`
