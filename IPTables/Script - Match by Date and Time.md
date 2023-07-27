1.  #!/bin/bash

3.  ##** MATCH BY DATE AND TIME **##

5.  ## See the help: iptables -m time --help

7.  # flushing the filter table
8.  iptables -F

11.  # !!!!! TIME is UTC and not system time

13.  # accepting incoming tcp port 22 (ssh) packets daily ONLY between 8:00-18:00 
14.  iptables -A INPUT -p tcp --dport 22 -m time --timestart 8:00 --timestop 18:00 -j ACCEPT
15.  iptables -A INPUT -p tcp --dport 22 -j DROP

18.  # accepting forwarded traffic (this is the Router) to www.ubuntu.com on workdays between 18:00-08:00
19.  iptables -A FORWARD -p tcp --dport 80 -d www.ubuntu.com -m time --weekdays Mon,Tue,Wed,Thu,Fri \
20.  --timestart 18:00 --timestop 8:00 -j ACCEPT

22.  # packets to www.ubuntu.com are dropped between 8:00 - 18:00 (working hours)
23.  iptables -A FORWARD -p tcp --dport 80 -d www.ubuntu.com -j DROP