Here's a script for a custom firewall on a web hosting server:

```
#!/bin/bash

# Flush all existing rules
iptables -F

# Set default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Allow traffic on loopback interface
iptables -A INPUT -i lo -j ACCEPT

# Allow established and related traffic
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow SSH traffic from a specific IP address
iptables -A INPUT -p tcp --dport 22 -s <your_IP_address> -j ACCEPT

# Allow HTTP and HTTPS traffic from anywhere
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Allow SMTP traffic from anywhere
iptables -A INPUT -p tcp --dport 25 -j ACCEPT
iptables -A INPUT -p tcp --dport 465 -j ACCEPT
iptables -A INPUT -p tcp --dport 587 -j ACCEPT

# Allow IMAP and POP3 traffic from anywhere
iptables -A INPUT -p tcp --dport 110 -j ACCEPT
iptables -A INPUT -p tcp --dport 143 -j ACCEPT
iptables -A INPUT -p tcp --dport 993 -j ACCEPT
iptables -A INPUT -p tcp --dport 995 -j ACCEPT

# Block all other incoming traffic
iptables -A INPUT -j DROP

# Allow outgoing traffic
iptables -A OUTPUT -j ACCEPT

# Save the rules
iptables-save > /etc/iptables/rules.v4

# Enable IP forwarding to allow NAT (if applicable)
echo 1 > /proc/sys/net/ipv4/ip_forward
```

This script sets the default policies to drop incoming and forwarded traffic, and allows outgoing traffic. It then allows traffic on the loopback interface and established/related traffic. Next, it allows SSH traffic from a specific IP address, and HTTP/HTTPS, SMTP, and IMAP/POP3 traffic from anywhere. All other incoming traffic is blocked. Finally, the script saves the rules to `/etc/iptables/rules.v4` and enables IP forwarding (if applicable).

You may need to customize this script for your specific needs, such as allowing traffic on additional ports or for specific applications. Make sure to test your firewall rules thoroughly before putting them into production.