## Introduction to RHEL

#### Managing systemd

### Objectives:

At the end of this episode, I will be able to:

1. Demonstrate how systemd is used to manage processes in RHEL.
2. Make configuration changes to systemd.
3. Differentiate between units and targets.
4. Identify systemctl commands that replace functionality previously offered undered SysVinit and Upstart.

### Files Involved

`/etc/rc.d`- This was the old sysv init system (systemd replaces it)

`/lib/systemd/system`- Text files end with extension that describe what they are (`httpd.service`)

### Diff between units and targets

`.target`- This is a collections of units (`.socket` `.service` `.path`)
`.unit`- This is the individual file

### Systemctl utility lets us manage systemd files

`sudo systemctl enable httpd.service`
`sudo systemctl start httpd.service`
`sudo systemctl enable --now httpd.service`

`sudo systemctl status httpd.service`

`sudo systemctl-analyze blame`

`init.d`
`rc0.d`- computer off
Run Level 1-`rc1.d`- Admin(S/U)- Only the admin no one else
`rc2.d`-
`rc3.d`- Multi-user no GUI
`rc4.d`-
`rc5.d`- Multi-User with GUI
`rc6.d` - Reboot
`rc.local`

## MAIN SYSTEMD DIR

`/lib/systemd/system/`
`ls *.target`

Each old run level = `.target`

`rc1 - s/u mode` = `rescue.target`

### To change runlevel

`sudo systemctl rescue` - = Single User Mode - One one user - Nothing will be locked

`sudo systemctl multi-user`

`sudo systemctl reboot`

### To change target by default

`sudo systemctl get-default` - will display what your `.target` is set at
`sudo systemctl set-default multi-user.target`

```Output

Removed /etc/sustemd/system/default.target
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/multi-user.target


```

### To change back to GUI

`sudo systemctl set-default graphical.target`
`sudo systemctl reboot`
