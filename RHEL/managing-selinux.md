## Security

#### Managing SELinux

### Objectives:

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/using_selinux/getting-started-with-selinux_using-selinux

At the end of this episode, I will be able to:

1. Define the basic functions of SELinux.
2. Install SELinux and verify that it is operational.
3. Differentiate between the various SELinux modes of operation.
4. Monitor logs to identify security policy violations.
5. Modify SELinux to allow for non-standard system access for third party applications.
6. Use SELinux to control access to the file system and network ports.

`sestatus`
![[Pasted image 20220611234034.png]]

- `Enforcing` mode is the default, and recommended, mode of operation; in enforcing mode SELinux operates normally, enforcing the loaded security policy on the entire system.
- In `permissive` mode, the system acts as if SELinux is enforcing the loaded security policy, including labeling objects and emitting access denial entries in the logs, but it does not actually deny any operations. While not recommended for production systems, permissive mode can be helpful for SELinux policy development and debugging.
- `Disabled` mode is strongly discouraged; not only does the system avoid enforcing the SELinux policy, it also avoids labeling any persistent objects such as files, making it difficult to enable SELinux in the future.

`sudo setenforce permissive`
`getenforce`
`sudo setenforce enforcing`

`sudo -s`

`tail /var/log/audit/audit.log`
`tail /var/log/audit/audit.log | grep httpd`

### How do you show the SELinux info for folder

`ls -lZ` - You use the cap z
![[Pasted image 20220612000439.png]]

### SElinux on process

`ps auxZ | grep httpd`
![[Pasted image 20220612000606.png]]

`chcon -Rv --type=<copy pasta> /website` - You copy and paste the `httpd_sys_content`
from the above `ls -lZ` command:
![[Pasted image 20220612001041.png]]

### If you want to tear it all down and remove the context back to default

`sudo restorecon -Rv /website`

### SELinux can handle ports as well as filepaths

`sudo semanage port -a -t http_port_t -p tcp 8080`- Autorizes any application allowed to access http ports will be allowed to access 8080.

## How do you see what ports you allow

`semanage port -l`
