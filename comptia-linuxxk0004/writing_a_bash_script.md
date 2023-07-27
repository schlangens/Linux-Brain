### Writing a Bash Script

#### What does a basic script look like?

---

- Example script
- Set execute permissions
  - `chmod +x ./sample.sh`
- Add folder to PATH if you wish to call it without entering the directory

```
#!/bin/bash
MESG="This is my message"
echo $MESG
```

#### What are some of the common commands we might use?

---

- Basic Commands:
  - `echo` - Displays text on screen
  - `echo -e` - Displays text on screen and then awaits user input
  - `read` - Copies user input in to a variable
  - `test` - Perform a comparison and return true or false
  - `seq` - Generate a list of numbers
  - `if/then/else` - Performs a calculation and then acts on the results

#### How many commands can we string together in a single script?

---

- Sample script to create a user account

```
#!/bin/bash
echo -e "Username:"
read username
if id -u $username > -1; then
	echo "That username already exists"
else
	echo -e "Full Name:"
	read fullname
	echo -e "Password:"
	read password
	useradd -c "$fullname" $username -p $password
	if id -u $username > -1; then
		echo "User created successfully"
	else
		echo "An error occurred while creating the user"
	fi
fi
```

#### Are there other logic commands like if/then?

---

- More Commands:

  - `for` - Perform an action for each entry in a list
  - `do` - Execute an action
  - `while` - Perform an action if certain conditions are met and loop

- Test if a user already has a home directory:

```
#!/bin/bash
echo -e "Username:"
read username
test -d /home/$username && echo "Home Directory Exists" || echo "Home Directory Does Not Exist"
```

```
* Solution #1: Sample script to create ten files called video#.mp4

#!/bin/bash
for filenum in `seq 10`
do
	touch video$filenum.mp4
done

* Solution #2: Sample script to create ten files called video#.mp4

#!/bin/bash
filenum=10
while [ $filenum -gt 0 ]
do
	touch video$filenum.mp4
	filenum=$(($filenum - 1))
done
```
