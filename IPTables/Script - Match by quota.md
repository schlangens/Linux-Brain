1.  #!/bin/bash

3.  ##** BUILD A DYNAMIC DATABASE OF BANNED IP ADDRESSES**##

5.  ## Get help: iptables -m recent --help

7.  iptables -F INPUT

10.  # when a packet is coming, it will be checked against this rule and
11.  # if its source ip belongs to the hacker list, the packet will be dropped
12.  # last seen time is updated with another 60 seconds (the source ip address stays in the list for another 60 seconds)
13.  iptables -A INPUT -m recent --name hackers --update --seconds 60 -j DROP

16.  # when the 1st matched packet arrives (tcp/25 between 8:00-10:00 UTC), a list named hacker is created,
17.  # the source ip address of the packet is added to that list and the packet is dropped
18.  iptables -A INPUT -p tcp --dport 25 -m time --timestart 8:00 --timestop 10:00 -m recent --name hackers --set -j DROP