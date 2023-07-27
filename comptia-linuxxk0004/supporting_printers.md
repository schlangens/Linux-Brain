### Supporting Printers

#### Do all Linux distributions handle printing the same way?

---

- CUPS - Common Unix Printing System
  - [https://www.cups.org/](https://www.cups.org/)
  - Developed by Apple
  - Provides a standard printing platform for Unix-like systems

#### What do we need to do to install CUPS?

---

- Installed by default on most distros
- Install CUPS
  - `sudo yum install cups`
  - or
  - `sudo apt install cups`
  - `sudo systemctl enable --now cups`

#### What printing protocols does CUPS support?

---

- `sudo lpinfo -v`
  - lpd
  - http/https
  - ipp/ipps
  - socket
  - serial
- Others can be added
  - `sudo yum install hplip`

#### How do we add a printer to CUPS?

---

- CUPS Web Administration
  1.  Browse to `http://127.0.0.1:631`
  2.  Select `Site Menu -> Administration`
  3.  Select `Add Printer`
  4.  Authenticate with an admin account
- CUPS CLI Administration
  1.  Place PPD file in `/etc/cups/ppd`
  2.  Create a printer
      - `sudo lpadmin -h localhost -p HPLaserJetM553 -E -v socket://10.0.10.50 -P /etc/cups/ppd/hp-color_laserjet_m553-ps.ppd`
      - `-h` The server hosting the printer
      - `-p` The name of the queue
      - `-E` Enable the printer
      - `-v` Device URI
      - `-P` Path to the PPD file

#### Now that we have a printer, how do we use it?

---

- GUI
  - Use application menus
- CLI
  - `lp -d HPLaserJetM553 ./file.txt`
  - `lpstat -p HPLaserJetM553`

#### Can you set a default printer from the CLI?

---

- `LPDEST=printername`

#### What other commands can we use to work with printers from the CLI?

---

| SysV Command | BSD Command | Description          |
| ------------ | ----------- | -------------------- |
| `lp`         | `lpr`       | Generate a print job |
| `lpstat`     | `lpq`       | View the print queue |
| `cancel`     | `lprm`      | Cancel a print job   |
