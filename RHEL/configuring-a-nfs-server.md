## Networking

#### Configuring a NFS Server

### Objectives:

At the end of this episode, I will be able to:

1. Install NFS on a RHEL server.
2. Configure shared folders in order to act as a NFS server.

`sudo dnf install nfs-utils`

`sudo systemctl enable --now nfs-server rpcbind`
`sudo systemctl status nfs-server`

## What versions of NFS do you support?

`sudo cat /proc/fs/nfsd/versions`

`sudoedit /etc/nfs.conf`

### Specify your folders to share

`mkdir ~/exports`

`mkdir /exports/backups /exports/share`
`cd /exports`

`sudoedit /etc/exports`

```config

/exports    10.0.0.1/24(rw,sync,root_squash)
/exports/share 10.0.0.1/24(rw,sync,root_squash)
/exports/backups 10.0.0.1/24(ro,sync,root_squash) 192.168.50.11(rw,no_root_squash)

```

`sudo exportfs -r` - Reload configuration. This will not kick the users out
`sudo exportfs -v` - verify your shares

### Open firewall

`sudo firewall-cmd --permanent --add-service rpc-bind`
`sudo firewall-cmd --permanent --add-service mountd`
`sudo firewall-cmd --permanent --add-service nfs`

### Reload firewall

`sudo firewall-cmd --reload`
