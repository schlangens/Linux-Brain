### Filtering Traffic with firewalld

#### Why would I use _firewalld_ over iptables?

---

- firewalld
  - Replacement for iptables
  - Both use the netfilter subsystem
  - Provides a simplified CLI

#### How do we know if we are running _firewalld_?

---

- Manage firewalld service
  - `systemctl start firewalld`
  - `systemctl enable firewalld`
- Determine firewall status
  - `firewall-cmd --state`

#### Where do we get started to configure the firewall?

---

- Determine default zone
  - `firewall-cmd --get-zones`
  - `firewall-cmd --get-default-zone`
- Change the default zone
  - `firewall-cmd --set-default-zone=block`
- View zone assignments
  - `firewall-cmd --get-active-zones`
- Create a custom zone
  - `firewall-cmd --permanent --new-zone=testlab`
  - `firewall-cmd --reload`
- View configuration for a zone
  - `firewall-cmd --list-all` for the default zone
  - `firewall-cmd --zone=work --list-all`

#### How do we assign a network interface to a zone?

---

- Assign an interface to a zone
  - `vi /etc/sysconfig/network-scripts/ifcfg-eno1`
  - `ZONE=work`
  - `systemctl restart network`
  - `systemctl restart firewalld`
  - `firewall-cmd --get-active-zones`

#### How do we use the zone to manage traffic?

---

- Allow a standard service through the firewall
  - `firewall-cmd --get-services` for a list of supported services
    - Default services are stored in `/usr/lib/firewalld/services/*.xml`
  - `firewall-cmd --zone=dmz --permanent --add-service=http`
  - `firewall-cmd --zone=dmz --permanent --list-services`

#### What if I want to manage non-standard traffic?

---

- Allow a non-standard service through the firewall
  - `firewall-cmd --get-services` for a list of supported services
    - Custom services can be added in `/etc/firewalld/services/*.xml`
  - `firewall-cmd --zone=dmz --permanent --add-port=8080/tcp`
  - `firewall-cmd --zone=dmz --permanent --list-ports`
  - Can also accept ranges like `10000-20000/udp`
