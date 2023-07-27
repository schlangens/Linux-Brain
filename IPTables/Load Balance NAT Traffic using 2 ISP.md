#!/bin/bash



To load balance traffic with two internet providers using IP Tables, you can create a firewall shell script with the following steps:

1. Create two routing tables with different names for each internet provider, for example, "provider1" and "provider2". You can do this using the "ip route add table" command.

```
ip route add default via <provider1_gateway> dev <provider1_interface> table provider1
ip route add default via <provider2_gateway> dev <provider2_interface> table provider2
```

Replace `<provider1_gateway>` and `<provider1_interface>` with the gateway and interface for your first internet provider, and `<provider2_gateway>` and `<provider2_interface>` with the gateway and interface for your second internet provider.

2. Set up policy-based routing rules to route traffic through the appropriate routing table based on the source IP address. For example, if traffic comes from the IP address range of 192.168.1.0/24, route it through the "provider1" routing table; otherwise, route it through the "provider2" routing table.

```
ip rule add from 192.168.1.0/24 table provider1
ip rule add from all table provider2
```

3. Set up NAT rules to translate the source IP address of outgoing traffic to the IP address of the interface that it's going out on. This ensures that return traffic will come back to the correct interface.

```
iptables -t nat -A POSTROUTING -o <provider1_interface> -j SNAT --to-source <provider1_ip>
iptables -t nat -A POSTROUTING -o <provider2_interface> -j SNAT --to-source <provider2_ip>
```

Replace `<provider1_interface>` with the interface for your first internet provider, `<provider1_ip>` with the IP address of that interface, `<provider2_interface>` with the interface for your second internet provider, and `<provider2_ip>` with the IP address of that interface.

4. Set up a load balancing rule using the "nth" match extension to evenly distribute outgoing traffic between the two internet providers. For example, if you want to distribute traffic between the two providers on a 50/50 basis, you can use the following command:

```
iptables -A OUTPUT -m state --state NEW -m nth --counter 0 --every 2 -j MARK --set-mark 1
iptables -A OUTPUT -m state --state NEW -m nth --counter 0 --every 2 -j MARK --set-mark 2
```

This rule will mark every other packet with a different mark, which can then be used to route the packet through the appropriate routing table.

5. Finally, set up a rule to use the appropriate routing table based on the packet's mark.

```
ip rule add fwmark 1 table provider1
ip rule add fwmark 2 table provider2
```

That's it! You can save this script and run it on your firewall to load balance traffic between two internet providers. Note that you may need to modify these commands to suit your specific network configuration.


# Another Script

1.  #!/bin/bash

3.  ##** LOAD BALANCE NAT TRAFFIC OVER 2 INTERNET CONNECTIONS WITH DYNAMIC IP ADDRESSES **##

5.  # Traffic that goes over the first connection
6.  # web: 80 443
7.  # email: 25 465 143 993 110 995
8.  # ssh: 22

10.  ISP1="22 25 80 110 143 443 465 993 995"

12.  # flushing nat table and POSTROUTING chain
13.  iptables -t nat -F POSTROUTING

15.  # enable routing
16.  echo "1" > /proc/sys/net/ipv4/ip_forward

18.  for port in $ISP1
19.  do
20.  iptables -t nat -A POSTROUTING -p tcp --dport $port -o eth1 -j MASQUERADE
21.  done

24.  # Traffic not NATed goes over the 2nd connection
25.  iptables -t nat -A POSTROUTING -o eth2 -j MASQUERADE
