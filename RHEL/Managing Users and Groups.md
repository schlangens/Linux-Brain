## Understanding 2 user accounts

- User accounts for services (1 - 999 )
  - User accounts for people -> `/bin/bash` & `sbin/nologin`

## Creating & managing users

`useradd --help`
`useradd <name>`

- This is written to `etc/passwd`
  `tail -n 1 /etc/passwd`
  `tail -n 1 /etc/shadow`

If you want to place a file in ALL the user(s) directory make sure to do that in `/etc/skel`

## User Properties

`usermod --help`

## User Configuration Files

`/etc/default/useradd`
`/etc/login.defs` - This trump everything over useradd
`/etc/skel/` - This goes to `$HOME` (all home folders for every user on server)
`/etc/passwd`
`/etc/shadow`
`/etc/group`
