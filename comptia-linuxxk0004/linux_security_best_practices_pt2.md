---
### Linux Security Best Practices (Part 2)

#### How do we enable SSH?
---

- SSH on most platforms is powered by OpenSSH
  - Installed by default
  - May need to be allowed through the firewall
  - Certificate authentication may need to be configured

#### How do we start hardening the SSH service?

---

- Disable SSHv1
  - `vi /etc/ssh/sshd_config`
  - `Protocol 2`
  - `systemctl restart sshd`
  - Take note of key names/locations
  - Server keys are stored in `/etc/ssh`
  - You will want to generate new keys

#### Why can't we keep the default keys?

---

- You cannot verify the strength of the default keys
  - Some distros (LiveCDs) use pre-packaged keys
  - Others generate keys prior to hardware RNGs kicking in
  - It is best to generate new ones.

#### How do we generate new keys?

---

- Generating new keys
  1.  Delete the key files (`rm -f /etc/ssh/*key*`)
  2.  `ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key`
  3.  `ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key`
  4.  `ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key`

#### What is the best way to distribute the public key to users?

---

- OpenSSH client configuration and usage
  - Public key is cached in `~/.ssh/known_hosts` for individual users
  - Cached in `/etc/ssh/ssh_known_hosts` for the entire system
  - If you receive a key before hand you can pre-load it
    - `/etc/ssh/ssh_host_ecdsa_key.pub`
    - `ssh-keyscan <host>`
    - `ssh-keyscan 192.168.0.100 >> ~/.ssh/known_hosts`
  - Viewing the fingerprint (on server)
    - `ssh-keygen -lf /etc/ssh/ssh_host_ecdsa_key.pub`
  - Can require key to pre-exist in `/etc/ssh/ssh_config`
    - `StrictHostKeyChecking`

#### Now that we have the key, how do we use it?

---

- Client connections
  - `ssh <username>@<hostname>`
  - `ssh -l <username> <hostname>`
  - Configuration file is `/etc/ssh/ssh_config`
  - Options
    - `-1` v1 Only
    - `-2` v2 Only
    - `-4` IPv4 Only
    - `-6` IPv6 Only
