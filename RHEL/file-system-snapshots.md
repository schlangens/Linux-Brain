## Storage

#### File System Snapshots

### Objectives:

At the end of this episode, I will be able to:

1. Use the SSM to create a snapshot of an LVM volume.
2. Mount a snapshot to access previous versions of files.
3. Restore a snapshot to rollback changes on a volume.

`ssm list`
![[Pasted image 20220611214306.png]]

### How do you take the snapshot?

`sudo ssm snapshot /dev/vg1/website` -- No user will be affected by this command :)

You dont want to many snapshots. Think of it like this. Do some work making any change to the data - snapshot it first

### How do you see your snapshots?

`sudo ssm list snapshots`
![[Pasted image 20220611214831.png]]

So this places a freeze on the data and then you branch with new. Say we want to restore something. We just tell our snapshot to continue and we end our branch.

### Restore - Umount first

`sudo umount /website`

``sudo lvconvert --merge <name of snapshot>
![[Pasted image 20220611215214.png]]

When you remount this fs it will have the old data.
`mount /dev/vg1/website /website`
