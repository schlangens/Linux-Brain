1.  #!/bin/bash

3.  # listing the filter table of all chains (INPUT, OUTPUT and FORWARD)
4.  iptables -t filter -L

6.  # listing the filter table (it's default) of all chains, verbose (v) and in numeric format (n)
7.  iptables -vnL

9.  # listing just a chain
10.  iptables -vnL INPUT

12.  # listing another table, not filter
13.  iptables -t nat -vnL

15.  # listing just a CHAIN
16.  iptables -t nat -vnL POSTROUTING