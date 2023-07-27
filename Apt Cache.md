`apt-cache search docx`

- will search the cache for all package names appropriate to the search term
  `apt-cache show docx2txt | less`
  `apt-cache show gcc | less`
- will show you detailed information about the package

`apt-cache search "web server"`

## Where does the Apt-Cache reside

`/var/lib/apt/lists`(the `apt-cache`)

## How do you update cache and upgrade it?

- The files in the cache must be the same as in the server

`sudo apt-get update && apt-get upgrade`

- `sudo apt-get update` updates your cache
- `sudo apt-get upgrade` upgrades all the software on your system.
- Make sure you update the cache before you upgrade!

## Install software

`apt-cache search xeyes`
`apt-cache show x11-apps`
`sudo apt-get install x11-apps`

## Installing from Source Code

`vi /etc/apt/sources.lst`

- Uncomment the following lines
  ![[Screen Shot 2022-06-07 at 10.25.59 PM.png]]

`sudo apt-get update`
`sudo apt-get install dpkg-dev`

`sudo apt-get source x11-apps`

## Uninstall Applications

`sudo apt-get remove <package name>` - This will leave configuration files after removal of package

- The preferred way is to purge

`sudo apt-get purge <package name>`- removes config file and package
`sudo apt-get autoremove <package name>` - This will remove dependencies as well

`cd /var/cache/apt/archives`

- Clean these up by doing the following
  `sudo apt-get clean`- Deletes ALL compressed package archives
  `sudo apt-get autoremove` - removes unwanted dependencies
  `sudo apt-get autoclean` - deletes package archives no long accessible
