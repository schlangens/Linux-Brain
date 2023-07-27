1.  #!/bin/bash

3.  ###*** FIREWALL FOR A DESKTOP OPERATING SYSTEM ***###

5.  #flush filter table from all chains
6.  iptables -F

8.  #allow loopback interface traffic
9.  iptables -A INPUT -i lo -j ACCEPT
10.  iptables -A OUTPUT -o lo -j ACCEPT

13.  #drop invalid packets on INPUT and OUTPUT CHAINS
14.  iptables -A INPUT -m state --state INVALID -j DROP
15.  iptables -A OUTPUT -m state --state INVALID -j DROP

18.  #optional, uncomment the line if you want to allow incoming connections from our LAN
19.  #iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT

21.  #optional, uncomment the line if you want to allow incoming ssh connection from a specific ip address
22.  #iptables -A INPUT -p tcp --dport 22 --syn -s 80.0.0.1 -j ACCEPT

24.  #allow only ESTABLISHED and RELATED packets on INPUT
25.  iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

27.  #allow also NEW packets on OUTPUT (packets that initialize connections)
28.  iptables -A OUTPUT -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

31.  #set policy to DROP on INPUT and OUTPUT CHAINS
32.  iptables -P INPUT DROP
33.  iptables -P OUTPUT DROP