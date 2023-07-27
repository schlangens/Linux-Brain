
1.  #!/bin/bash

3.  # flushing the firewall
4.  iptables -F

6.  # dropping all traffic from 100.0.0.1
7.  iptables -A INPUT -s 100.0.0.1 -j DROP

9.  # accepting all ssh traffic from network 80.0.0.0/16
10.  iptables -A INPUT -s 80.0.0.0/16 -p tcp --dport 22 -j ACCEPT

12.  # dropping all outgoing HTTPS traffic to www.ubuntu.com (dns traffic must be permitted)
13.  iptables -A OUTPUT -p tcp --dport 443 -d www.ubuntu.com -j DROP