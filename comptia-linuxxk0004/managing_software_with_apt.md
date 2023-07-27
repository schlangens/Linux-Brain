### Managing Software with Apt

#### Is apt different than apt-get?

---

- `apt-get`
  - Older package manager
  - `apt-cache` used to maintain package cache
- `apt`
  - Newer package manager
  - Combines package and cache management in one tool

#### Where does the software were installing actually come from?

---

- Gets packages from a package repository
- `/etc/apt/sources.list`

#### Can we see the list of software available in the repo?

---

- Search package names
  - `apt list <name>`
- Full regex search
  - `apt search <criteria>`

#### Once we have found our software, how do we install it?

---

- `apt install`
  - Installs a package

#### What if the software we want isn't in the repo?

---

1. Add the new repo to sources.list
   - `vi /etc/apt/sources.list`
   - `deb http://download.webmin.com/download/repository sarge contrib`
2. Import the signing key
   - `wget http://www.webmin.com/jcameron-key.asc`
   - `apt-key add jcameron-key.asc`
3. Update and install the new software
   - `apt update`
   - `apt install webmin`

#### Does apt automatically update software when new versions are released?

---

- `apt update`
  - Gets package update information
  - Updates the cache
- `apt upgrade`
  - Upgrades all installed packages
- `apt dist-upgrade`
  - Upgrades operating system packages

#### How can we remove software if we no longer need it?

---

- `apt remove`
  - Removes a package
