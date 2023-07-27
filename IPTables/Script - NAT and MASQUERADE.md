1.  #!/bin/bash

3.  # flush the nat table of all chains
4.  iptables -t nat -F

7.  # enable routing process
8.  echo "1" > /proc/sys/net/ipv4/ip_forward

11.  # define rules that match traffic that should be NATed
12.  # we perform NAT for the entire subnetwork
13.  # enp0s3 is the external interface
14.  # 80.0.0.1 is the public & static ip address
15.  iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o enp0s3 -j SNAT --to-source 80.0.0.1

18.  # if the public IP address is dynamic we use MASQUERADE instead of SNAT
19.  # iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o enp0s3 -j MASQUERADE

22.  # it's not mandatory to perform NAT for entire subnet. We could perform NAT only for some protocols
23.  # Example: we perform NAT only for TCP
24.  # iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -p tcp -o enp0s3 -j SNAT --to-source 80.0.0.1

26.  # filtering is done on FORWARD CHAIN