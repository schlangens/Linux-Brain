## Storage

#### Choosing a File System

### Objectives:

At the end of this episode, I will be able to:

1. Define the primary features of XFS and ext4.
2. Select the appropriate file system based on a scenario.

   ### Ext4 FS

   - Default in RHEL6 and earlier
   - Journaling - If we lose power/or drive powers down during a write and it is have way done writing that file IT WILL NOT DESTROY THE FILE. Only when its 100 percent done does the file get removed
   - - FS up to 50 TB - 50 TB is not big in the enterprise world. This was the reason the fs changes in later releases.
   - Extent-based Metadata - This means it stores the metadata in a very efficient manner which is great for CPU loads
   - Online Deframentation -
   - Online Resizing - Grow and Shrink the drive

### XFS FS

- Default since RHEL7
- Journaling
- FS up to 1024 TB (1 PB)
- Concurrent Ops - Multithreaded IO - 2 disc at the same time great for SSD
- Integrated Backup/Restore
- Online Defrag
- Online Resizing (Grow only)

### When to choose ext4?

- Single-threaded I/O
- Limited Resources
  - Less than 1000 IOPS
  - Less than 200MB/s bandwidth
  - Limited CPU availability
- Support for shrinking

### When to choose XFS

- Multi-threaded I/O
- Large amounts of storage (50TiB+)
- Video workloads
- You have no preference
