## Introduction to RHEL

#### Managing Software Repositories

### Objectives:

At the end of this episode, I will be able to:

1. Describe how repositories are managed.
   1. Redhat manages the repository
2. Add and remove new repositories.
3. Temporarily enable or disable repositories.

`sudo dnf repolist all`
`sudo dnf list httpd`

`/etc/yum.repos.d`

### create a new repo and name whatever you want

`sudoedit wemin.repo`

```config
[Webmin]
name=Webmin Distribution Neutral
#baseurl=https://download.webmin.com/download/yum
mirrorlist=https://download.webmin.com/download/yum/mirrorlist
enabled=1
```

### Download 3rd party key and trust

`wget https://download.webmin.com/jcameron-key.asc`
`rpm --import jcameron-key.asc`

- Now DNF will do your updates

`sudo dnf update`

### Disable the repo

`sudoedit /etc/yum.repos.d/webmin.repo`

```config
[Webmin]
name=Webmin Distribution Neutral
#baseurl=https://download.webmin.com/download/yum
mirrorlist=https://download.webmin.com/download/yum/mirrorlist
enabled=0
```

`sudo dnf list webmin`

### Quickly & Temporarily Enable Repo to install 3rd party

`sudo dnf list webmin --enablerepo=Webmin`

### External Resources:

- [Webmin](http://www.webmin.com/rpm.html)
