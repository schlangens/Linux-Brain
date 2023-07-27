1.  #!/bin/bash

3.  # flushing the firewall
4.  iptables -F

6.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.10 -j DROP
7.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.11 -j DROP
8.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.12 -j DROP
9.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.13 -j DROP
10.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.14 -j DROP
11.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.15 -j DROP
12.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.16 -j DROP
13.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.17 -j DROP
14.  #iptables -A INPUT -p tcp --dport 25 -s 10.0.0.18 -j DROP

17.  # all 9 rules obove are replaced by the following rule:
18.  iptables -A INPUT -p tcp --dport 25 -m iprange --src-range 10.0.0.10-10.0.0.18 -j DROP