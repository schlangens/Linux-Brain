`cat 1> output.txt`# Truncate (del) if anything is in file
`cat 1>> output.txt` # Appends to file

> Standard Input = 0
> Standard Output = 1
> Standard Error = 2

`cat -k bla 2>> error.txt`

`cat 1>> output.txt 2>>error.txt`

## Standard Input (Read from file)

`cat 0< input.txt`
`cat < input.txt`

`cat 0< input.txt 1> hell.txt`
`cat < input.txt > hello.txt`

`tty` # Where this terminal is located on system

![[Screen Shot 2022-06-02 at 10.00.18 PM.png]]

> On another terminal we can send our standard output to another terminal

`cat 0< input.txt > /dev/pts/1`

- Standard Input, Standard Output and Standard Error are Data Streams.
- Using redirection you can control where those streams "flow"
