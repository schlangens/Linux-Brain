1.  #!/bin/bash

3.  # -A -> appends a rule at the end of the CHAIN
4.  iptables -A OUTPUT -p tcp --dport 443 -j DROP

7.  # -I -> inserts a rule on top (1st position) of the CHAIN
8.  iptables -I OUTPUT -p tcp --dport 443 -d www.linux.com -j ACCEPT

10.  # -F -> flushes the CHAIN
11.  iptables -t filter -F OUTPUT

14.  # -Z -> zeroises the packet and byte counters
15.  iptables -t filter -Z

17.  # -D -> deletes a rule
18.  iptables -D OUTPUT 2

20.  # -P -> sets the default POLICY
21.  iptables -P INPUT ACCEPT

23.  # -N -> creates a user-defined CHAIN
24.  iptables -N TCP_TRAFFIC

26.  # -X -> delete a user-defined CHAIN
27.  iptables -X TCP_TRAFFIC