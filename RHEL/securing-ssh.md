## Security

#### Securing SSH

### Objectives:

At the end of this episode, I will be able to:

1. Restrict which users may access the system using SSH.
2. Configure key-based authentication and disable password authentication.
3. Change the default port used by sshd.

`/etc/ssh`
![[Pasted image 20220612233000.png]]
`ssh_config` - is the client configuration
`sshd_config` - is the server configuration

`sudoedit /etc/ssh/sshd_config`

```config

AllowUsers sschlangen

```

- If more than 1 user put them in a group like so

```config


AllowGroups ssh-enabled

```

- By using groups we dont need to restart the daemon because the service will check the file periodically

- Else restart the service

`sudo systemctl restart sshd`

### Certificate Based Authentication

`whoami`
`ssh-keygen`

- Send copy to the server
  `ssh-copy-id sschlangen@10.0.0.11`

- To verify the key is on the server check out
- `~/.ssh/authroized_keys`

- If you need to point to the correct key file do this
- `ssh sschlangen@10.0.0.11 -i ~/.ssh/id_rsa.pub`

### Now turn off password-auth

`sudoedit /etc/ssh/sshd_config`

`/password`
![[Pasted image 20220612234618.png]]

```config


PasswordAuthentication no


```

### If you want to change the port

`sudoedit /etc/ssh/sshd_config`
`/Port`
![[Pasted image 20220613000148.png]]

```config
#Port 22
Port 2222

```

### Add firewall and SELinux

`sudo firewall-cmd --add-port=2222/tcp`
`sudo firewall-cmd --add-port=2222/tcp --permanent` - \* Note you must run both these commands in sequence for firewall-cmd

`sudo semanage port -a -t ssh_port_t -p 2222`

`sudo systemctl restart sshd`

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/pdf/security_hardening/red_hat_enterprise_linux-8-security_hardening-en-us.pdf
