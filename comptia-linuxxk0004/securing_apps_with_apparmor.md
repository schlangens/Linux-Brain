### Securing Apps with AppArmor

#### How is AppArmor different from SELinux?

---

- AppArmor
  - Similar to SELinux
    - SELinux targets inodes
    - AppArmor targets paths
  - Default for Debian/Ubuntu

#### How do we know if we are running AppArmor?

---

- Test if AppArmor is installed
  - `apparmor_status`
- Verify AppArmor polices are loaded
  - `apt policy apparmor`
- Install AppArmor tools if needed
  - `apt-get install apparmor-utils`

#### How is AppArmor configured?

---

- AppArmor Profiles
  - Each app has a profile
  - `/etc/apparmor.d/<path_to_command`
  - `/etc/apparmor.d/bin.nc`
- Profile Modes
  - Complain
    - Logs
  - Enforce
    - Logs and prevents

#### Are there any global settings, or is everything done per app?

---

- AppArmor Tunables
  - Allow modifying other behaviors
  - `/etc/apparmor.d/tunables/`

#### Which applications do we need to secure?

---

- Anything with open network sockets
- List applications without a profile
  - `aa-unconfined`

#### How do we enable AppArmor for an app?

---

- Enable AppArmor for Apache2
  1.  Install the Apache AppArmor module
      - `apt install libapache2-mod-apparmor`
  2.  Generate a Profile
      - `aa-genprof apache2`
  3.  Enable AppArmor
      - `aa-enforce /etc/apparmor.d/usr.sbin.apache2`
      - Could also use
        - `aa-complain`
        - `aa-disable`
  4.  Follow any additional instructions in the profile
      - `cat /etc/apparmor.d/usr.sbin.apache2`
  5.  Restart Apache
      - `systemctl restart apache2`
