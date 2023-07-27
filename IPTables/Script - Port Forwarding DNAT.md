1.  #!/bin/bash

3.  ### PORT FORWARDING (DNAT) ###

5.  # Port Forwarding is always done on the PREROUTING chain

7.  # flushing nat filter of PREROUTING chain
8.  iptables -t nat -F PREROUTING

11.  # all the packets coming to the public IP address of the router and port 80
12.  # will be port forwarded to 192.168.0.20 and port 80
13.  iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.0.20

16.  ## VARIANTS

19.  # 1.redirect port 8080 to port 80
20.  # Internet clients connect to the public IP address of the router and port 8080 and the packets are
21.  # redirected to the private server with 192.168.0.20 and port 80
22.  iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.0.20:80

26.  #2. Load-Balancing
27.  # On all 5 private servers (192.168.0.20-192.168.0.24)run the same service (e.g. HTTPS)
28.  # The router will pick-up a random private IP from the range and then translate and send (port-forward) the packet to that IP
29.  iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.0.20-192.168.0.24