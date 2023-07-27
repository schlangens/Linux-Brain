### Filtering Traffic with iptables

#### How do we know if we are running _iptables_?

---

`systemctl status iptables`
`systemctl enable --now iptables`

#### Can we switch from _firewalld_ to _iptables_?

---

- `yum install -y iptables-services`
  - Sometimes called `iptables-persistent` or just `iptables`
- `systemctl stop firewalld`
- `systemctl mask firewalld`
  - Disabling is not enough as a dependant service could still start it
- `systemctl enable --now iptables`
- `systemctl enable --now ip6tables`

#### Where do we get started configuring the firewall?

---

- List rules in a user-readable format
  - `iptables --list`
  - Use `-n` to skip name resolution
- List Rules in file syntax format
  - `iptables --list-rules`

#### How do the chains work together?

---

- Three chains
  - INPUT
    - Incoming traffic
    - Where most of our filtering is performed
  - FORWARD
    - Routed traffic
    - Not used on most machines
    - Typically used for routers/firewalls
  - OUTPUT
    - Outbound traffic
    - Not typically filtered for normal hosts

#### How do the rules work?

---

- Three actions
  - ALLOW - Permits the connection
  - DROP - Discards any connection traffic without notifying the sender
  - REJECT - Discards any connection traffic and notifies the sender

#### How do we manage incoming traffic?

---

- Using the `iptables` command
  - `iptables -A INPUT -p tcp --dport ssh -j DROP`
  - `iptables -A INPUT -p tcp --dport ssh -s 10.10.10.10 -m state --state NEW,ESTABLISHED -j ACCEPT`
  - `iptables -A INPUT -p tcp --sport ssh -m state --state ESTABLISHED -j ACCEPT`
  - Save changes
    - `iptables-save` or `iptables save`
  - Discard changes
    - `iptables -F`

#### Does everything have to be done with the iptables command?

---

- Modifying the `iptables` configuration file
  - `/etc/sysconfig/iptables` and `ip6tables`
  - `systemctl restart iptables`
- Bidirectional Control Example
  - `iptables -A OUTPUT -p tcp -d 172.16.0.1 --dport 3306 -m state --state NEW,ESTABLISHED`
  - `iptables -A INPUT -p tcp --sport 3306 -m state --state ESTABLISHED -j ACCEPT`

#### Can we monitor what iptables is doing?

---

- You can test connections manually
- Tools like _nmap_ can help as well
- Log option
  - You can create a duplicate rule with the _log_ action
  - `iptables -A INPUT -p tcp --dport ssh -j DROP`
  - `iptables -A INPUT -p tcp --dport ssh -j LOG`
- Statistics can be monitored with the _watch_ command
  - `iptables -vnL --line`
  - `watch -n 0.5 iptables -vnL`
