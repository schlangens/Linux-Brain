### Managing File Permissions

## How do we see what file permissions are set on a file?

**Viewing Permissions**

`ls -l`

**Identities**

| Letter | Identity |
| ------ | -------- |
| u      | User     |
| g      | Group    |
| o      | Others   |

**Permissions**

| Symbol | Permission |
| ------ | ---------- |
| -      | None       |
| r      | Read       |
| w      | Write      |
| x      | Execute    |

![[Pasted image 20220615073820.png]]

#### Weren't the permissions set with numbers in the past?

---

**Numerical Values**

| Number | Attribute |
| ------ | --------- |
| 4      | Read      |
| 2      | Write     |
| 1      | Execute   |

**Numerical Notation**

| Notation | Permissions             |
| -------- | ----------------------- |
| 0        | None                    |
| 1        | Execute                 |
| 2        | Write                   |
| 3        | Write and Execute       |
| 4        | Read                    |
| 5        | Read and Execute        |
| 6        | Read and Write          |
| 7        | Read, Write and Execute |

## How do we modify the permissions?

- `chmod`
  - Assign/remove permissions
  - Typical default:
    - `rwxr-xr-x`
    - `755`
  - `chmod u+x <file>`
  - `chmod u=rwx,g-rx,o+r <file>`
  - `chmod -R 755 <folder>`

#### Where do the default permissions come from?

---

- umask
  - Sets default permissions for new file
  - `/etc/profile` for all users
  - `~/.bashrc` for one user
- Typical Default
  - Typical: `umask 022`
  - Files
    - `rw-rw-r--`
    - `664`
  - Folders
    - `rwxrwxr-x`
    - `775`

#### Do we use the same numerical notation with umask?

---

**umask Values**

| Value | Result                  |
| ----- | ----------------------- |
| 0     | Read, Write and Execute |
| 1     | Read and Write          |
| 2     | Read and Execute        |
| 3     | Read Only               |
| 4     | Write and Execute       |
| 5     | Write Only              |
| 6     | Execute Only            |
| 7     | no Permissions          |

#### How do we define who the owner or group is?

---

- `chown`
  - Change the owner of a file
  - `chown <user> <file>`
  - `chown <user>:<group> <file>`
- `chgrp`
  - Change the group of a file
  - `chgrp <group> <file>`
