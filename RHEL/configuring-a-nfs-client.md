## Networking

#### Configuring a NFS Client

### Objectives:

At the end of this episode, I will be able to:

1. Install the NFS client on a RHEL system.
2. Connect to NFS shares located on other systems.

### Install Client - Should be install by default

`sudo dnf install nfs-utils -y`

### If supporting NFS 2 or 3 start RPCBIND servive

`sudo systemctl status rpcbind`
`sudo systemctl enable --now rpcbind`

### Look for NFS server?

`showmount -e 10.0.0.11`

### Mount the NFS share??

`cd /mnt`
`mkdir <folder on local drive>`
`sudo mount -t nfs 10.0.0.11:/folder/to/mount /folder/on/local`

### Force version

`sudo mount -t nfs -0 vers=4 10.0.0.11:/folder/to/mount /folder/on/local`

### Make perm

`sudoedit /etc/fstab`- This is the Filesystem Table file

```config

10.0.0.11:/folder/to/mount /folder/on/local nfs defaults,rw,sync 0 0

```

### Want to see the mount points?

`df -h`
