## Troubleshooting

#### Monitoring System Performance

### Objectives:

At the end of this episode, I will be able to:

1. Quickly monitor processor, memory, disk and network utilization from the CLI.
2. Use the Cockpit service to visually monitor performance from a web browser.
3. Describe how tools like OProfile, PCP and tuned can further be used to troubleshoot performance.

### CPU - Memory - Disk IO / Network Bandwidth

## Show whats running

`sudo ps aux`
`top` - Refreshed 2-5 second - Allows you to sort `P`
`df -h`
`du -sh ~/`
`free -h`

### Cockpit

If you do min or custom install most likely cockpit not installed. If you run a full install cockpit is most likey installed by default

`sudo dnf install cockpit cockpit-dashboard -y`

`sudo systemctl enable --now cockpit.socket`

- Listens on port 9090 by default
- web server uses ssl
- `firewall-cmd --permanent --add-port=9090/tcp`
- `firewall-cmd --add-port=9090/tcp`
- Login with your user account for the system
- You will see what you have access 2 - check the reuse my password..
- ![[Pasted image 20220613022929.png]]

### Things to look at

- Omonitor
- pcp - performance co-pilot
- tunedd - performance tune
