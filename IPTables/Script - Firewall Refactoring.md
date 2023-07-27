1.  #!/bin/bash

3.  # flushing all chains
4.  iptables -F

6.  # deleting all user-defined chains
7.  iptables -X

9.  # allow all outgoing traffic (except invalid packets)
10.  iptables -A OUTPUT -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

13.  # allow incoming ssh packets
14.  iptables -A INPUT -p tcp --dport 22 -j ACCEPT
15.  iptables -A OUTPUT -p tcp --sport 22 -j ACCEPT

18.  #create a new chain named ACCEPTED_MAC
19.  iptables -N ACCEPTED_MAC

21.  #add rules to the user defined-chain
22.  iptables -A ACCEPTED_MAC -m mac --mac-source B8:81:98:22:C7:6B -j ACCEPT
23.  iptables -A ACCEPTED_MAC -m mac --mac-source B8:81:98:22:C6:7C -j ACCEPT
24.  iptables -A ACCEPTED_MAC -m mac --mac-source B8:81:98:22:23:AB -j ACCEPT
25.  iptables -A ACCEPTED_MAC -m mac --mac-source B8:81:98:22:67:AA -j ACCEPT

28.  # jump from the INPUT chain to the user-defined chain
29.  # now packets traverse the iptables rules in the user-defined chain
30.  iptables -A INPUT -j ACCEPTED_MAC

32.  #if not dropped or accepted (terminating target) packets continue traversing the INPUT chain
33.  iptables -A INPUT -p icmp -j ACCEPT
34.  iptables -A OUTPUT -p icmp -j ACCEPT

37.  iptables -P OUTPUT DROP
38.  iptables -P INPUT DROP