### Super User Privileges

## When do we need super user privileges?

- System-wide changes
- Changes that affect other users
- Configuring some services

## What is the easiest way to access super user privileges?

- `su`
  - Substitute user
- `su -`
  - Switch to root
  - `-` loads normal environment
- `su - <username>`
  - Switch to user

## What if I just want to perform a single command?

- `sudo <command>`
  - Executes command as root
  - Password cached for five minutes by default

## Who is allowed to use the sudo command?

- User must be authorized to run sudo
  - In some distros (like Ubuntu) simply add 'sudo' group as a secondary group
  - In others (like Red Hat) you must create your own group and add it to `/etc/sudoers`
- `visudo <user/group> <machine>=<commands>`
- `dpezet ALL=(ALL) NOPASSWD:ALL`

## What would it look like if we only wanted to grant access to a few commands?

- `%techsupport localhost=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom`

## Are there any shortcuts or aliases to help with all this?

- `sudoedit`
  - Useful when editing a single write-protected file
  - `sudoedit /etc/hosts`
