- You can join files together using the `cat` command.
- use the pager program `less` to page through large amounts of output

`cat file.txt`
`tac file.txt`

`cat file[1-5].txt`
`cat file[1-5].txt | tac`
`cat file[1-5].txt | tac > reversed.txt`

`tac myfile.mp3 > myresversedfile.mp3`

`cat file[1-5].txt | rev`

![[Screen Shot 2022-06-06 at 10.54.36 PM.png]]

`tac` reverses a file vertically
`rev` reverses a file horizontally

- You can jumbo some shit up by doing the followng:

`cat file[1-5].txt | tac | rev`

![[Screen Shot 2022-06-06 at 10.56.37 PM.png]]

## Pager programs

`cat file[1-5].txt | head -n 2` # By default will show top 10 lines
`cat file[1-5].txt | less`
`cat file[1-5].txt | tail`

`head -n 20 /etc/cups/cups-browsed.conf`

`cat file[1-5].txt | tail -n 2`
`tail -n 20 /etc/cups/cups-browsed.conf`

`head -n 20 /etc/cups/cups-browsed.conf | tail -n 1`
`head -n 2- /etc/cups/cups-browsed.conf | tail -n 3`
