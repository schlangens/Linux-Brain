1.  #!/bin/bash

3.  iptables -F INPUT

6.  ### FILTER BY PORT (-p tcp|udp --sport | --dport) ###

8.  # ALLOW SSH CONNECTIONS ONLY FROM ONE IP ADDRESS
9.  # dropping incoming packets to port 22 except if they are coming from 80.0.0.1
10.  iptables -A INPUT -p tcp --dport 22 -s 80.0.0.1 -j ACCEPT
11.  # it's possible to specify port using service name (/etc/services)
12.  # iptables -A INPUT -p tcp --dport ssh -s 80.0.0.1 -j ACCEPT

14.  # dropping all other ssh traffic
15.  iptables -A INPUT -p tcp --dport 22 -j DROP

17.  # allowing DNS Queries
18.  iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
19.  iptables -A INPUT -p udp --sport 53 -j ACCEPT

22.  ### FILTER BY PROTOCOL (-p) ###

24.  # dropping incoming GRE traffic
25.  iptables -A INPUT -p gre -j DROP

27.  # allowing outgoing ICMP traffic
28.  iptables -A OUTPUT -p icmp -j DROP

31.  ### FILTER BY INTERFACE (-i | -o) ###

33.  # allowing loopback interface traffic (always recommended)
34.  iptables -A INPUT -i lo -j ACCEPT
35.  iptables -A OUTPUT -o lo -j ACCEPT

37.  # dropping ssh traffic that's coming on eth0 interface (suppose it's external)
38.  iptables -A INPUT -p tcp --dport 22 -i eth0 -j DROP

40.  # allowing ssh traffic that's coming on eht1 interface (suppose it's internal)
41.  iptables -A INPUT -p tcp --dport 22 -i eth1 -j ACCEPT

43.  # allowing outgoing https traffic via eth1
44.  iptables -A OUTPUT -p tcp --dport 443 -o eth1 -j ACCEPT