1.  #!/bin/bash

3.  echo "### BLOCKING ALL IPs AND NETWORKS FROM FILE."

5.  # a file called bad_hosts.txt exists in the same directory with the script and
6.  # contains IPs and Networks, one per line like:
7.  # 11.0.0.16
8.  # 8.8.8.8
9.  # 1.2.3.4
10.  # 192.0.0.0/16

14.  # File that contains the IPs and Nets to block
15.  FILE="bad_hosts.txt"

17.  # Creating a new set
18.  ipset -N bad_hosts iphash -exist

20.  # Flushing the set if it exists
21.  ipset -F bad_hosts

24.  echo "Adding IPs from $FILE to bad_hosts set:"
25.  for ip in `cat $FILE`
26.  do
27.  ipset -A bad_hosts $ip
28.  echo -n "$ip "
29.  done

31.  # Flush iptables if you run this script more than once to avoid duplicate rules
32.  # iptables -F

34.  # Adding the iptables rule that references the set and drops all ips and nets
35.  echo -e -n "\nDropping with iptables... "
36.  iptables -I INPUT -m set --match-set bad_hosts src -j DROP
37.  echo "Done"