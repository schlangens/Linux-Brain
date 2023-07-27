1.  #!/bin/bash

3.  #1. Set the ACCEPT POLICY an all CHAINS
4.  iptables -P INPUT ACCEPT
5.  iptables -P OUTPUT ACCEPT
6.  iptables -P FORWARD ACCEPT

8.  #2. Flush all tables from all CHAINS
9.  iptables -t filter -F
10.  iptables -t nat -F
11.  iptables -t mangle -F

13.  #3. Delete user-defined CHAINS (if there is any)
14.  iptables -X