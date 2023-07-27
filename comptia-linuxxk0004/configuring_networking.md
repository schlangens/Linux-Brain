Filename: comptia-linuxxk0004-10-2-1-configuring_networking
Show Name: CompTIA Linux+ (XK0-004)  
Topic: Managing Networking  
Episode Name: Configuring Networking  
Description: In this episode, Zach and Don demonstrate how to configure a network adapter in Linux. They show how to manually configure IP settings via network scripts and then demonstrate how to do the same using the NetworkManager service found in many distros.

---

### Configuring Networking

#### How can we view our current network configuration?

---

- Viewing Configuration
  - `ip addr`
  - `ifconfig`
  - `ip route`

#### Is there anything we should do before we start changing things?

---

- DHCP
  - `dhclient`
  - `dhclient -r`
- Restarting the network service
  - Most changes require restarting the network service
  - `service network restart`
  - `systemctl restart network.service`

#### Where are the network interface configurations stored?

---

- Configuration using interface scripts
  - Stored in `/etc/sysconfig/network-scripts`
  - First part of name
    - `en` = Ethernet
    - `wl` = Wireless
    - `ww` = Cellular (WWAN)
  - Second part of name
    - `o` = On-board
    - `p` = PCI card
    - `s` = Hotplug slot
  - `/etc/sysconfig/network-scripts/ifcfg-eno1`

```
DEVICE=eno1
TYPE=Ethernet
BOOTPROTO=none
IPADDR0=192.168.0.2
PREFIX0=24
GATEWAY0=192.168.0.1
DEFROUTE=yes
DNS1=8.8.8.8
ONBOOT=yes
```

#### What about global settings like DNS servers?

---

- Configuration using global settings
  - `/etc/sysconfig/network`
    - Configurations that apply to all NICs
    - `GATEWAY=192.168.0.1`
  - Name Lookups
    - `/etc/resolv.conf`
      - DNS Servers
      - Shouldn't be modified if using the Network Manager
      - NM copies DNS settings from the `ifcfg` files
        when the service starts
    - `/etc/hosts`
      - Overrides DNS
  - Host Name
    - `/etc/hostname`
      - `hostname <name>` is not normally persistent
      - Defines a machines hostname
      - To modify:
        - `hostnamectl set-hostname <name>`
      - To verify:
        - `hostnamectl status`

#### Are there any easier ways to configure network settings?

---

- Configuring using NetworkManager
  - Viewing Status
    - `nmcli device status`
    - `nmcli device show <int_name>`
    - `nmcli connection show`
    - `nmcli connection show <int_name>`
  - Reseting an Adapter
    - `nmcli connection reload`
    - `nmcli connection down <int_name>`
    - `nmcli connection up <int_name>`
  - Configuring an Adapter
    - `nmcli connection edit <int_name>`
    - `set connection.autoconnect yes`
    - `set ipv4.method manual`
    - `set ipv4.addr 192.168.0.2/24`
    - `set ipv4.dns 8.8.8.8`
    - `set ipv4.gateway 192.168.0.1`
    - `save <temporary/persistent>`
    - `quit`
