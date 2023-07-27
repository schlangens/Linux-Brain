## What are tarballs?

- Tarbells are `containers` to store files in for compression
- Tarballs can be compressed using various compression algorithms.
- `gzip` and `bzip2` are common options as well as `xz`
-

## Create a tarball - no compression

`tar -cvf ourarchive.tar file[1-3].txt`

## View whats in a tar file

`tar -tf ourarchive.tar`

## Extract a tar

`tar -xvf ourarchive.tar`

![[File+Archiving+Cheat+Sheet.pdf]]

## Compression

`gzip ourarchive.tar`
`bzip2 ourarchive.tar`

## Confirm Compression

`file ourarchive.tar.gz`
`file ourarchive.tar.bz2`

## Reverse Compression

`gunzip ourarchive.tar.gz`
`bunzip2 ourarchive.tar.bZ2`

## How do you create a zip file

`zip ourthing.zip file1.txt file2.txt file3.txt`

## Can we do this in 1 step?

`tar -cvzf ourarchive.tar.gz file[1-3].txt`
`tar -cvjf ourarchive.tar.bz2 file[1-3].txt`

`tar -xvzf ourarchive.tar.gz`
`tar -xvjf ourarchive.tar.bz2`

## Resources

https://www.rootusers.com/gzip-vs-bzip2-vs-xz-performance-comparison/

`touch hungry.sh`
`echo "I am hungry, Feed me data" >> ~/demands.txt`
`date >> ~/demands.log`
`*/1 * * * * ~/hungry.sh`
