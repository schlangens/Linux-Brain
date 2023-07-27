1.  #!/bin/bash

3.  ##** FILTER BY MAC ADDRESS (only source) **##

5.  iptables -F INPUT

7.  # defining a variable that contains the allowed MAC addresses
8.  PERMITTED_MACS="08:00:27:15:b2:ec 08:00:27:15:b2:df 08:00:27:15:b2:ab"

10.  # this host can communicate only with other hosts inside our LAN that have
11.  # a MAC address from this list
12.  # !!! to be able to communicate outside the LAN (e.g. Internet) the MAC
13.  # of the router internal interface should also be allowed
14.  for MAC in $PERMITTED_MACS
15.  do
16.  iptables -A INPUT -m mac --mac-source $MAC -j ACCEPT
17.  echo "$MAC permitted"
18.  done

21.  # set POLICY to DROP on INPUT (all other packets are dropped)
22.  iptables -P INPUT DROP