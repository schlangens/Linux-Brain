## Remove it all

`rm -r /path/to/dir`

## If you want to delete 1 by 1 in folder

`rm -ri /path/to/dir`

## Make some random folders and files in each folder

`mkdir -p delfolder/deleteme{1,2,3}`
`touch delfolder/deleteme{1,2,3}/file{1,2,3}`

## Again

`mkdir -p delfolder/folder{1..3}`
`touch delfolder/folder{1,2}/file{1..10}.txt`
