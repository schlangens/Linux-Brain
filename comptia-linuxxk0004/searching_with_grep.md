### Searching with grep

#### What are regular expressions and how do they work with grep?

---

- Regular Expressions (RegEx)
  - Collection of wildcards
  - Widely supported
  - Not very user friendly
  - Understanding Regular Expressions

#### What do regular expressions look like?

---

- RegEx syntax
- `man 7 regex`

| Wildcard | Description              |
| -------- | ------------------------ | --- |
| `[ ]`    | List of possible values  |
| `-`      | Range of values          |
| `.`      | Any single character     |
| `*`      | Any number of characters |
| `^`      | Begining of line         |
| `$`      | End of line              |
| `        | `                        | Or  |
| `( )`    | Sub-expression or slice  |
| `\`      | Escape character         |

#### How do we use regular expressions to search for data?

---

- `grep`
  - **G**lobally Search a **R**egular **E**xpression and **P**rint
  - Searches files for a string
  - Two modes
    1. Fixed Strings (Default)
       - `grep -F`
       - `fgrep`
    2. Extended Regular Expression
       - `grep -E`
       - `egrep`

#### Can you show us an example of searching with grep?

---

**Lab File (cal-2019.txt)**

```
01/01/2019 New Year's Day
07/04/2019 Independence Day
10/31/2019 Halloween
12/25/2019 Christmas
```

**Searching for files containing Halloween**

```
grep -r Halloween ~/
```

**Searching for lines in a file containing Halloween**

```
cat ~/cal-2019.txt | grep Halloween
```

#### What if we want to search for more than one string, is that where regular expressions come in?

---

**Searching for more than one string in a file**

```
cat ~/cal-2019.txt | grep -E "Halloween|Christmas"
```

**Searching for a range of values in a file**

```
cat ~/cal-2019.txt | grep -E "^1[0-2]"
```
