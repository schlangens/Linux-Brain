### Managing Groups

## What command do we use to create groups?

- `groupadd <groupname>`
- `/etc/group`

## Are we able to modify the group once it is created?

- `groupdel <groupname>`
- `groupmod <groupname>`
  - `-n` Rename group
  - `groupmod -n <new_name> <old_name>`

## How do we put user accounts into the groups?

- `gpasswd`
  - Add a user
    - `gpasswd -a <user> <group>`
  - Remove a user
    - `gpasswd -d <user> <group>`
  - Add a group admin
    - `gpasswd -A <user> <group>`

## Are secondary group permissions applied automatically?

- Users perform all actions under their primary group by default
- `newgrp <groupname>` temporarily changes that context
- `chgrp`/`chown` can also be used
- `groups <username>` to see group membership

## Are there any other ways to verify a group's configuration?

- Getting information
  - `getent passwd <user>`
  - `getent shadow <user>`
  - `getent group <group>`
  - `groups <user>`
