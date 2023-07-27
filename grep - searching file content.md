## What is Grep?

- A search through files and standard output (CTRL + F)
- `grep`returns lines that contain a piece of text (wildcards work too)
- `-c` option will return the line count.
- `-i`option will search in case insensitive manner (Linux is case-sensitive OS by default)
- `-v` option will invert the search (do the opposite)

`grep e hello.txt`
`grep -ic a gedsby_manuscript.txt`
`grep -i "our boys" gadsby_manuscript.txt`

`grep -v e gadsby_manuscript.txt` # Find all the lines that dont have a "v"
`grep -vc e gadsby_manuscript.txt`

`grep -ci "e" gadsby/gadsby_manscruopt.txt hello.txt`

![[Screen Shot 2022-06-07 at 1.29.11 AM.png]]

`ls -F /etc | grep -v / > files.txt`

`man -k print | grep files`
