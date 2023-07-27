### Understanding TCP/IP

#### How are IP addresses assigned?

---

- IP Address / Subnet Mask
  - IP Address: 192.168.0.1
  - Subnet Mask: 255.255.255.0
    - Class A - 255.0.0.0 - 16,777,214 Hosts
    - Class B - 255.255.0.0 - 65,534 Hosts
    - Class C - 255.255.255.0 - 254 Hosts

#### How do we choose which addresses to use?

---

- Private IPs (RFC 1918)
  - 10.x.x.x
  - 172.16.x.x -> 172.31.x.x
  - 192.168.0.x -> 192.168.255.x
- Public
  - Class A - 1.0.0.0 -> 126.255.255.255
  - Class B - 128.0.0.0 -> 191.255.255.255
  - Class C - 192.0.0.0 -> 223.255.255.255

#### What about IPv6? I hear that it is significantly different.

---

- IPv4 Characteristics
  - 32 bit address
  - ~4.3 Billion addresses
- IPv6 Characteristics
  - 128 bit address
  - 3.4 x 10^38 addresses
  - Integrated IPSec
  - IP Mobility
  - Extensible Headers

#### We've been talking about IP, but where does TCP come in?

---

- TCP
  - Transmission Control Protocol
  - Reliable transport mechanism
- UDP
  - User Datagram Protocol
  - Best-effort transport mechanism
- ICMP
  - Internet Control Management Protocol
  - Ping and other troubleshooting and status protocols

#### Can we see all of this happening in the background?

---

**Port Number Lab**

1. Determine the IP for a server
   - `nslookup itpro.tv`
   - `ftp.dell.com`
   - `towel.blinkenlights.nl`
2. Look for existing connections
   - `ss -an | grep 192.124.249.2`
3. Browse to the web site from step 1
4. Look for existing connections
   - `ss -an | grep 192.124.249.2`

#### What port numbers should we be familiar with?

---

**Common TCP/UDP Ports**

| Port Number | Protocol | TCP/UDP |
| ----------- | -------- | ------- |
| 20          | FTP      | TCP     |
| 21          | FTP      | TCP     |
| 22          | SSH      | TCP     |
| 23          | TELNET   | TCP     |
| 25          | SMTP     | TCP     |
| 53          | DNS      | TCP/UDP |
| 80          | HTTP     | TCP     |
| 110         | POP3     | TCP     |
| 119         | NNTP     | TCP     |
| 123         | NTP      | UDP     |
| 139         | NetBIOS  | TCP/UDP |
| 143         | IMAP     | TCP     |
| 161         | SNMP     | UDP     |
| 443         | HTTPS    | TCP     |
| 465         | SMTP-SSL | TCP     |
| 993         | IMAPS    | TCP     |
| 995         | POP3S    | TCP     |
