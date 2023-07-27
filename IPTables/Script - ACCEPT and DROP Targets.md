1.  #!/bin/bash

4.  #flushing the filter table of all chains
5.  iptables -F

8.  # ACCEPT target is terminating one. If the packet is accepted, no other rule will evaluate the packet
9.  # ACCEPTing incoming ssh packets (port tcp/22) from any IP address
10.  iptables -A INPUT -p tcp --dport 22 -j ACCEPT

12.  # DROP any other tcp packets 
13.  iptables -A INPUT -p tcp -j DROP

16.  # DROP is a terminating target. If a packet was dropped by the last rule, no other rule will evaluate the packet

18.  # the next rule will never be evaluated. No packet will be matched against it.
19.  iptables -A INPUT -p tcp --dport 80 -j ACCEPT