## Troubleshooting

#### Monitoring System Logs

### Objectives:

At the end of this episode, I will be able to:

1. Use dmesg logs to troubleshoot hardware devices.
2. Use syslog logs to troubleshoot services and applications.
3. Configure log rotation to prevent losing log messages.
4. Configure rsyslog to create a centralized logging server.
5. Describe how journald supplements syslogd in RHEL 8.

### For hardware logs use `dmesg`

`sudo dmesg | less`

### For software logs `syslog`

`/var/log/messages`
`sudo less /var/log/messages`
`sudo tail -f /var/log/messages`

### Edit log rotation

`/etc/logrotate.conf`

### If you want to send logs somewhere use rsyslog

`sudo dnf list rsyslog*`

`/etc/rsyslog.conf`

```config

*.*@@<ip address>:514

```

`sudo systemctl restart rsyslog`

### Journald is going to be taking over soon

`sudo journalctl`
If you want to use journald you will need to turn on persistent
`sudo mkdir /var/log/journal`
`sudo systemctl restart systemd-journald`

`sudo journalctl -n 10`
![[Pasted image 20220613030118.png]]

## Follow the journal

`sudo journalctl -f`
![[Pasted image 20220613030223.png]]

`sudo journalctl -p err`
![[Pasted image 20220613030348.png]]

`sudo journalctl --since <specify time range> --until=<specify end date>`

- Check to make sure logs are writing to disc when changing to journald. `/var/log/journal`
