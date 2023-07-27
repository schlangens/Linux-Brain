## What are aliases?

Easy to remember nicknames for your pipeline.
Aliases go in `.bash_aliases` in your home folder.
A `.` as the start of a filename makes that file "hidden"
aliases are accessible when you restart your terminal. Make sure the first command can be piped to `xargs`

## Syntax for alias

`alias AliasName="command1 -options args | command2 --options args ..."`

`vim .bash_aliases`

```shell

alias getdates='date | tee /home/user/fulldate.txt | cut --delimiter=" " --fields=1 | tee /home/user/shortdate.txt | xargs echo hello'

alias calmagic="xargs cal -A 1 -B 1 > /home/user/thing.txt"

```

- You can use aliases in other aliases

`cal -A 1 -B 1`

![[Screen Shot 2022-06-02 at 11.06.47 PM.png]]

`echo "10 1985" | calmagic` # This would show the month before and after October of 1985
