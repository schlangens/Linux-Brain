### Securing Apps with SELinux

#### What is SELinux?

---

- Security Enhanced Linux (SELinux)
  - Adds fine grained mandatory access control to Linux
  - Goes far beyond basic UNIX UGO file permissions
  - Allows you to restrict what files and paths software is able to access

#### What does SELinux do when it detects inappropriate access?

---

- SELinux Modes
  - _Enforcing_ - Access not conforming to ACLs is blocked
  - _Permissive_ - Access not conforming to ACLs is logged
  - _Disabled_ - ACLs are not applied

#### So how do we get started with configuring SELinux?

---

- Working with SELinux
  - Verify status of SELinux
    - `sestatus`
  - Define status at time of boot
    - `vi /etc/selinux/config`
  - Modify status temporarily
    - `setenforce enforcing` or `setenforce 1`
    - `setenforce permissive` or `setenforce 0`
    - `getenforce` to verify
  - View SELinux log
    - `tail /var/log/audit/audit.log`
  - View SELinux context for a process or file
    - `ps auxZ | grep httpd`
    - `ls -laZ /var/www/html/index.html`
    - `ls -ldZ /website`

#### Can you show us an example of configuring a service?

---

1. Create a non-standard folder for a service
   - `mkdir /website`
   - `vi /website/test.html`
   - `vi /etc/httpd/conf/httpd.conf`
   - Change DocumentRoot and Default Document Folder to `/website`
   - `systemctl restart httpd`
2. Test access to the content
   - `http://127.0.0.1/test.html`
   - `tail -f /var/log/audit/audit.log | grep httpd`
3. Correct the security context and test again
   - `chcon -Rv --type=httpd_sys_content_t /website`
   - `systemctl restart httpd`
4. Reset the path to default context
   - `restorecon -Rv /website`

#### Are these changes persistent?

---

- `chcon` is persistent
  - `restorecon` resets the values, erasing the changes
  - Unfortunately, people use `restorecon` a lot
  - Can accidentally erase context
- SELinux policy
  - The SELinux policy tracks the default contexts that `restorecon` uses
  - Can be overridden
    - `/etc/selinux/targeted/contexts/files/file_contexts.local`
  - To update the policy, use `semanage fcontext...`
    - Part of the `policycoreutils-python` package
  - Example
    1. `ls -dZ /website`
    2. `semanage fcontext -a -t httpd_sys_content_t /website`
    3. `restorecon -Rv /website`
    4. `ls -dZ /website`
  - Making it recursive
    1. `semanage fcontext -a -t httpd_sys_content_t "/website(/.*)?"`

#### Is there anything else SELinux is capable of?

---

`semanage port -a -t http_port_t -p tcp 8080`
`semanage port -l`
