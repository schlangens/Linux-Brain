Depending on what distribution you are running the `locate` command may not come pre-installed. Ubuntu 20.04 appears to have this issue, for example, but Ubuntu 18.04 does not.

If you find you are having issues, try installing the `locate`  and `mlocate` packages from your repositories.

`sudo apt install locate`

`sudo apt install mlocate`

## Build current DB

`sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.locate.plist`

## Update the DB

`sudo updatedb`

## Get info on current DB after building

`locate -s`

```

Scotts-MacBook-Pro:~ sschlangen$ locate -S



Database: /var/db/locate.database

Compression: Front: 13.58%, Bigram: 55.47%, Total: 9.39%

Filenames: 943577, Characters: 104060431, Database size: 9775343

Bigram characters: 4353031, Integers: 87466, 8-Bit characters: 168


```

## Bckup db to desktop of current user

`locate -s > ~/Desktop/db.before`

## Check to see if .conf exist

`locate -e *.conf`
`locate --existing *.conf`

## To check symbolic links for issues

`locate --follow *.conf`

## MIsc Resources

https://osxdaily.com/2011/11/02/enable-and-use-the-locate-command-in-the-mac-os-x-terminal/
