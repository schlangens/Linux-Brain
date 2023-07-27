1.  #!/bin/bash

3.  echo "### BLOCKING CHINA ###"

6.  # Check if the file exists (in the current directory) and if yes, remove it
7.  if [ -f "cn-aggregated.zone" ]
8.  then
9.  rm cn-aggregated.zone
10.  fi

12.  # Download the aggregate zone file for China
13.  wget http://www.ipdeny.com/ipblocks/data/aggregated/cn-aggregated.zone

16.  # Check if there was an error
17.  if [ $? -eq 0 ]
18.  then
19.  echo "Download Finished!"
20.  else
21.  echo "Download Failed! Exiting ..."
22.  exit 1

24.  fi

26.  # Creating a new set called china of type hash:net (nethash)
27.  ipset -N china hash:net -exist

29.  # Flushing the set
30.  ipset -F china

34.  # Iterate over the Networks from the file and add them to the set
35.  echo "Adding Networks to set..."
36.  for i in `cat cn-aggregated.zone`
37.  do
38.  ipset -A china $i
39.  done

43.  # Adding a rule that references the set and drops based on source IP address
44.  echo -n "Blocking CN with iptables ... "
45.  iptables -I INPUT -m set --match-set china src -j DROP
46.  echo "Done"