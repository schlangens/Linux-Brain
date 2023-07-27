### Configuring Bash

#### Where can we find the configuration files for Bash?

---

- Login scripts:
  - `/etc/profile`
  - `/etc/profile.d/*`
  - `~/.profile`
  - `~/.bash_profile`
- Bash configuration:
  - `/etc/bashrc`
  - `~/.bashrc`
- Logout script
  - `~/.bash_logout`

#### What is an example of something we would want to configure?

---

- Search path for executables defined:
  - Globally in `/etc/profile`
  - Per user in `~/.profile` or `~/.bash_profile`

#### Are all variables configured the same way?

---

- When setting a variable, they are typically local to that specific shell instance.
  - Local variable is tied to the session
    - `EXAMPLE="Hello"`
    - `echo $EXAMPLE`
  - Use export to convert them to global
    - `export MESG`
  - Add the following command to your .profile to make this automatic:
    - `set -o allexport`
  - View variables
    - `env`

#### Are there any variables that behave differently?

---

- Aliases
  - Add these to the .bashrc to automate commands
    - `alias ls='ls --color=auto'`
    - `alias ls='ls --color=auto -la'`
    - `unalias ls`

####

---

- Functions
  - Add to .bashrc to create custom command sets
  - Can combine multiple commands in to a single command
  - Example system status function:

```
    function sysinfo()
    	{
			echo -e "\nKernel Information:" ; uname -a
			echo -e "\nOS Version:" ; cat /etc/centos-release
			echo -e "\nSystem Uptime:" ; uptime
			echo -e "\nMemory Utilization:" ; free -m
			echo -e "\nFilesystem Utilization:"; df -h
    	}
```

Execute with `sysinfo`

#### Is there a way to make these settings available to all users?

---

- Update `/etc/skel/.bashrc` to populate values for new users
