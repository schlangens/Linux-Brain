## Security

#### Configuring firewalld

### Objectives:

At the end of this episode, I will be able to:

1. Define the basic functions of firewalld, firewall-cmd and the netfilter service.
2. Configure and manage firewall zones.
3. Permanently or temporarily allow services to communicate through the firewall

`sudo -s`

`firewall-cmd --state`
`systemctl status firewalld`
`systemctl enable --now firewalld`

By default server can reach out, and will only allow a little in

- IPv6
- PING

Everything in firewalld is managed by zones. Zones are collections adapters
`firewall-cmd --get-zones`
![[Pasted image 20220612164642.png]]
Rhel puts all in 1 defaulkt zone
`firewall-cmd --fet-default-zone`
![[Pasted image 20220612164816.png]]

### Create a new firewall zone

`firewall-cmd --new-zone=ss-media --permanent`

### Read the new zone we created

`firewall-cmd --reload`

### Make it default by flagging it

`firewall-cmd --set-default-zone=ss-media`

### Add interface into the new zone

`firewall-cmd --get-active-zones`

- Edit the adapter and flap
  `nmcli connection modify ens160 connection.zone ss-media`
  `nmcli connection down ens160`
  `nmcli connection up ens160`

## Show zones and rules

`firewall-cmd --list-all`

`firewall-cmd --zone=public --list-all`

## List services already built by them

``firewall-cmd --get-services
![[Pasted image 20220612165942.png]]

`firewall-cmd --zone=ss-media --add-service=http --permanent`
`firewall-cmd --zone=ss-media --add-service=https --pernanent`

### Open port in firewall

`firewall-cmd --zone=ss-media --add-port=8888/tcp`

`firewall-cmd --zone=ss-media --list-all`

### If you want something custom you will need to create the rules.

`/usr/lib/firewalld/services/`

- You could create a custom XML file
- Make your edits in the following dir:
- `/etc/firewalld/services`
