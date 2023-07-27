## Networking

#### Network Manager CLI

### Objectives:

At the end of this episode, I will be able to:

1. Configure and monitor your network configuration using the nmcli command.

`systemctl status NetworkManager`

`sudo dnf install NetworkManager -y`

`sudo systemctl enable --now NetworkManager`

`nmcli`

`nmcli device status`

`nmcli device show ens160` - This is a great little cheatsheet for setting names

`sudo nmcli connection show`
`sudo nmcli connection show ens160`

`sudo nmcli connection edit ens160`

### nmcli interface command prompt (Setting static IP)

`set ipv4.method manual`
`set ipv4.addr 192.168.1.69/24`
`set ipv4.dns 8.8.8.8`
`set ipv4.gateway 10.0.0.1`

`save`
`save persistent`
`quit`

`sudo nmcli connection reload`- Reloads configurations on every adapter. They do not go offline

### Flap interface

`sudo nmcli connection down ens160`
`sudo nmcli connection up ens160`
