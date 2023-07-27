### Linux Security Best Practices (Part 1)

#### What operational activities fall within cybersecurity?

---

- CIA Triad [DIAGRAM 38]
  - Confidentiality
  - Integrity
  - Availability

#### Are there specific technologies we should be deploying?

---

- Not one size fits all
- Many options exist
- Example: Authentication
  - PINs, Passwords and Passphrases
  - Tokens and One-time Passwords
  - Biometrics
  - RADIUS and TACACS+
  - LDAP
  - Kerberos

#### So we just pick the one that most closely matches our need?

---

- Multi-factor Authentication [DIAGRAM 39]

#### Do attackers always focus on user credentials?

---

- Typical steps for an attacker:
  1.  Discover a system
  2.  Enumerate services
  3.  Gain a foothold
  4.  Establish persistence
      - Privilege escalation
  5.  Cover your tracks

#### How can we stop or minimize an attack?

---

- `chroot` Jails [DIAGRAM 40]
  - Restricts an app's file access
  - Creates a false root (/) folder
- File and access auditing
  - `yum install audit`
  - `systemctl enable auditd`
  - `/etc/audit/audit.rules`
  - `/var/log/audit/audit.log`
  - `ausearch --start today --loginuid 500`
  - `aureport --start 04/14/2019 00:00:00 --end 04/15/2019 00:00:00`

#### What about physical security? Couldn't they just steal our computer?

---

- Encryption [DIAGRAM 41]
  - Provides confidentiality
- Hashing [DIAGRAM 42]
  - One-way, non-reversable encryption
- Linux solutions
  - LUKS Disk Encryption
  - SSL/TLS
  - OpenVPN
  - IPSec
  - GPG

#### Can we see an example of using LUKS?

---

- Linux Unified Key Setup (LUKS)
- Enabling LUKS
  1. Clean the target disk
     - `shred -v --iterations=1 /dev/sdb1`
  2. Enable LUKS on the disk
     - `cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb1`
  3. Verify disk shows as encrypted
     - `blkid /dev/sdb1`
  4. Mount and format the disk
     - `cryptsetup luksOpen /dev/sdb1 storage`
     - `mkfs.xfs /dev/mapper/storage`
     - `mount /dev/mapper/storage /mnt/storage`

#### What other types of encryption should we be using?

---

- SSH (Covered in Part 2)
