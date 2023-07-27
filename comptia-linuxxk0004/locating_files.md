### Locating Files

#### What is your go-to method to find files?

---

- `find` command
- `find [path...] [expression...]`

**Search by filename**

```
find / -name README.txt
find / -name '*.txt' 2>/dev/null
```

#### Can you search by something other than a file name?

---

**Search by Permission Mode**

```
find /bin -perm +rwx
find /bin -perm -rwx
```

**Search by File Size**

```
find /usr -size 2M
find /usr -size 2c
find /usr -size -2c
find /usr -size +20M
```

**Search by Group**

```
find / -group dpezet
find / -gid 1002
```

**Search by User ID**

```
find /home/dpezet -user dpezet
find /home/dpezet -uid 1002
```

#### Can we limit the number of subdirectories it searches?

---

**Restrict Search Depth**

```
find / -maxdepth 6 -name README.txt
```

#### Are there any other tools we could use to look for files?

---

- `locate` command
  - `locate README`
- `whereis` command
  - `$ whereis ls`
  - `whereis ifconfig`
- `which` command
  - Returns ONLY the 1st match it finds by default
  - `which xterm`

#### What if none of those commands find a file I am looking for?

---

- `type` command
  - Displays how a command is interpreted
    - `type cat`
    - `type ls`
  - `type -a ls`
- `grep` command
  - Searches within files
  - Uses regular expressions
  - Covered later
