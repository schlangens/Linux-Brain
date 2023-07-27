## How to use the find command's default behaviour

`find`

- Find does not use a DB. Works right off the FS.
- The downside is it is slightly slower.

`find ~/Documents`

## How to control search depth

`find . -maxdepth 1`

## How to search by type (files or dir)

`find . -type f` = Returns just the files
`find . -type d` = Returns just folders

## You can combine these commands

`find . -maxdepth 3 -type. d `

## How to search by name

`find . -name "5.txt"`

## How to search by file size

`find / -type f -size +100k`
`find / type f -size +100k | wc -l`
`find / type f -size -5M | wc -l`
`sudo find / -type f -size -100k size +5M | wc -l`
`sudo find /f -tyoe f - size -100k -o -size +5M | wc -l`

## Copy the files it finds from search to that folder

`sudo find / -type 5 -size +100K -size -5M -exec cp {} ~/Desktop/search-results.txt \;`

`sudo find / -maxdepth 3 -type f -size +100k -size -5M -ok cp {} ~/Desktop/copy_here \;`

## Create some random folders and files and places a txt file inside the range of folders randomly.

`mkdir haystack`
`mkdir haystack/folder{1..500}`
`touch haystack/folder{1.500}/file{1..100}`
`touch haystack/folder$(shuf -i 1-500 -n 1)/needle.txt`

## Use the find command to find the needle.txt

`find haystack -type f -name "needle.txt" -ok cp {} ~/Desktop \;`
