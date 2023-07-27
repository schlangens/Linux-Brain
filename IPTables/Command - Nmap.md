1.  ##** SCAN ONLY YOUR OWN HOSTS AND SERVERS !!! **##
2.  ## Scanning Networks is your own responsibility ##

4.  # Syn Scan - Half Open Scanning (root only)
5.  nmap -sS 192.168.0.1

7.  # Connect Scan
8.  nmap -sT 192.168.0.1

10.  # Scanning all ports (0-65535)
11.  nmap -p- 192.168.0.1

13.  # Specifying the ports to scan
14.  nmap -p 20,22-100,443,1000-2000 192.168.0.1

16.  # Scan Version
17.  nmap -p 22,80 -sV 192.168.0.1

19.  # Ping scanning (entire Network)
20.  nmap -sP 192.168.0.0/24

22.  # Excluding an IP
23.  nmap -sS 192.168.0.0/24 --exclude 192.168.0.10

25.  # Saving the scanning report to a file
26.  nmap -oN output.txt 192.168.0.1

28.  # OS Detection
29.  nmap -O 192.168.0.1

31.  https://nmap.org/book/performance-timing-templates.html

33.  -T paranoid|sneaky|polite|normal|aggressive|insane (Set a timing template)
34.  These templates allow the user to specify how aggressive they wish to be, while leaving Nmap to pick the exact
35.  timing values. The templates also make some minor speed adjustments for which fine-grained control options do
36.  not currently exist.

38.  # -A OS and service detection with faster execution
39.  nmap -A -T aggressive cloudflare.com