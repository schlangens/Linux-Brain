### Managing Software with Yum/DNF

#### What is the difference between yum and dnf?

---

- `yum` is the "Yellowdog Update Manager"
- `dnf` is "Dandified YUM"
- Basic syntax is identical between the two
- `dnf` improvements:
  - Fully documented API
  - Better dependency handling

#### Where does the software were installing actually come from?

---

- Repositories
  - Defined in `/etc/yum.repos.d/*`
  - Eventually will move to `/etc/dnf/dnf.conf`

#### Can we see the list of software available in the repo?

---

- Finding software
  - `yum list httpd` (search by name)
  - `yum search httpd` (search by keyword)
- Viewing information about a package
  - `yum info httpd`

#### Once we have found our software, how do we install it?

---

- Installing software
  - `yum install httpd`

#### What if the software we want isn't in the repo?

---

1. Add the new repo to reposd
   - `vi /etc/yum.repos.d/webmin.repo`
2. Import the signing key
   - `wget http://www.webmin.com/jcameron-key.asc`
   - `rpm --import jcameron-key.asc`
3. Install the new software
   - `yum install webmin`

```
[Webmin]
name=Webmin Distribution Neutral
#baseurl=http://download.webmin.com/download/yum
mirrorlist=http://download.webmin.com/download/yum/mirrorlist
enabled=1
```

#### Does yum automatically update software when new versions are released?

---

- Perform updates
  - `sudo yum update -y`

#### How can we remove software if we no longer need it?

---

- Removing software
  - `dnf remove httpd`
  - `dnf autoremove`
  - `yum erase httpd`
