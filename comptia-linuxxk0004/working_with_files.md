### Working with Files

#### How do we perform simple operations like viewing a list of files?

---

- `ls`
  - `-l` List view
  - `-a` Display all files, including hidden
  - `-h` Display human friendly file sizes

| Color           | Description                 |
| --------------- | --------------------------- |
| Default color   | Normal/text file            |
| Blue            | Directory                   |
| Sky blue        | Symbolic link or audio file |
| Green           | Executable file             |
| Yellow on Black | Device                      |
| Pink            | Image file                  |
| Red             | Archive file                |
| Red on Black    | Broken link                 |

#### How do we view the contents of a file?

---

- `cat`
  - Displays file contents to stdout
  - Not paginated
  - `sudo cat /var/log/messages`
- `more`
  - Same as cat, but paginated
- `less`
  - Same as more, but allows bidirectional scrolling

#### What if we only want to see the top or bottom of the file?

---

- `head`
  - Displays first 10 lines
  - `sudo head /var/log/messages`
  - `sudo head -n 5 /var/log/messages`
- `tail`
  - Displays last 10 lines
  - `sudo tail /var/log/messages`
  - `sudo tail -n 5 /var/log/messages`
  - `sudo tail -f /var/log/messages`

#### How would we go about moving a file to a different location?

---

- `touch`
- `cp`
  - `cp -R ~/myfiles /opt/myfiles`
- `mv`
  - `mv ~/file1 /opt/mylist`
- `rm`
  - `rm -R ~/myfiles`

#### Are directories handled the same way as files?

---

- `mkdir`
- `rmdir`
