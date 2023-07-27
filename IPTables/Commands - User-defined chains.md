1.  # creating a user-defined chain
2.  iptables -N TCP_TRAFFIC

4.  # add rules to the chain
5.  iptables -A TCP_TRAFFIC -p tcp -j ACCEPT

7.  # jump to the chain from the input chain
8.  iptables -A INPUT -p tcp -j TCP_TRAFFIC

10.  # flush all rules in the chain
11.  iptables -F TCP_TRAFFIC

13.  # delete the chain
14.  iptables -X TCP_TRAFFIC