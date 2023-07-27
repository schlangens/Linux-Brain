
1.  #!/bin/bash

3.  iptables -F INPUT

5.  # allow only 1 incoming ping (echo-request) per second with a burst of 3
6.  iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/sec --limit-burst 3 -j ACCEPT
7.  # drop packets that were not accepted by the rule above (they are above the limit)
8.  iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

11.  # allow only 5 new incoming connections per second to port 443 (https)
12.  iptables -A INPUT -p tcp --dport 443 --syn -m limit --limit 5/sec -j ACCEPT
13.  iptables -A INPUT -p tcp --dport 443 --syn -j DROP