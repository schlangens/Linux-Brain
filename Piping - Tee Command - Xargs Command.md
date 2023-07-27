- Piping connects `STDOUT` of one command to the `STDIN` of another
- Redirection of `STDOUT` breaks pipelines
- To save a data "snapshot". without breaking pipelines, use `tee`
- If a command doesnt accept `STDIN`, but you want to `|` use `xargs`
- Commands you use w `xargs` can still have their own arguments

`date >> date.txt`
`cut < date.txt --delimiter " " --fields 1`

![[Screen Shot 2022-06-02 at 10.12.03 PM.png]]

`date | cut < date.txt --delimiter " " --fields 1`

`date | cut < date.txt --delimiter " " --fields 1 > today.txt`

-- Redirection can occur in between the different arguments/options

`date | cut < date.txt > today.txt --delimiter " " --fields 1`

## How does the TEE command work?

![[Screen Shot 2022-06-02 at 10.25.01 PM.png]]

-- Allows us to save the flow to a file and "pass the flow down"

` date | tee fulldate.txt | cut --delimiter=" " --fields=1`

-- Once you have redirected (> ) you can not pipe ( | ) anymore

`date | xargs echo`

## What if a command does not accept standard input and only accepts command arguments (echo)?

- You would need to use `xargs` command to convert to command argument so `echo` can use it

![[Screen Shot 2022-06-02 at 10.40.47 PM.png]]

> If you pass argument to xargs and date (xargs goes first)
