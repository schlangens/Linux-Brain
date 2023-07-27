1.  #!/bin/bash

3.  # By default POLICY is ACCEPT on all CHAINS

5.  # !!! If there is no rule that accepts packets and the policy is set to drop, all traffic will be dropped.
6.  # Change the default policy with caution!

8.  # Setting the DROP Policy on FORWARD chain
9.  iptables -P FORWARD DROP

11.  # Setting the ACCEPT Policy on OUTPUT chain
12.  iptables -P OUTPUT ACCEPT

14.  # Setting the DROP Policy on INPUT chain
15.  iptables -P INPUT DROP