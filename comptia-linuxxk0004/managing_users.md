### Managing Users

## What command do we use to create a user account?

- `useradd <username>`
  - `-c` Full Name
  - `-e` Expiration date
  - `-s` Default shell
  - `-d` Home directory
- `useradd jdoe -c "John Doe" -e 2019/12/31 -s /bin/dash -d /home/john_doe`

## What if we make a mistake? Can we modify the user?

- `userdel <username>`
  - Use `-r` to remove their files as well
- `usermod`
  - Rename account: `usermod -l jdoe jsmith`
  - Lock account: `usermod -L jdoe`
  - Unlock account: `usermod -U jdoe`
  - Add user to group: `usermod -a -G Marketing`

* `chsh`
  - Prevent an account from logging in interactively
  - e.g. `chsh -s /bin/nologin <username>`

## What is the default password for the user?

- `passwd <username>`
- `chage <username>`
  - Define password expiration policy
  - Display current info
    - `chage -l jdoe`
  - Modify policy
    - `chage -m <mindays> -M <maxdays> -E <expiredate> -W <warndays> jdoe`

## Where do all the default values come from?

- `useradd -D` displays defaults
- /etc/login.defs
- /etc/default/useradd
- /etc/skel

## How can we verify a user account's configuration?

- /etc/passwd
  - Defines accounts
  - User ID
  - UIDs typically start at 500
  - Users/Groups can share an ID (not ideal)
- /etc/shadow
- /etc/group
- `getent` (Covered later)
