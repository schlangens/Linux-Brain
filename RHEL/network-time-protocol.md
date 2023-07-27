## Networking

#### Network Time Protocol

### Objectives:

At the end of this episode, I will be able to:

1. Configure a RHEL server to use NTP as a time source.
2. Verify your time configuration.

`sudo timedatectl`
`sudo timedatectl list-timezones`
`sudo timedatectl set-timezone America/New_York`

`sudo timedatectl set-time 15:00`

`systemctl status chronyd`

`sudo /etc/chrony.conf`

```config

pool 2.rhel.pool.ntp.org iburst


```

### Turn off NTP

`sudo timedatectl set-ntp false`

`sudo systemctl restart chronyd`

`chronyc sources`
