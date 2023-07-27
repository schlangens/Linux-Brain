### Editing Files with vi

![[Pasted image 20220617140529.png]]

#### Can you give us a basic overview of how vi works?

---

- vi (and vim)
  - `:`
    - Command mode
  - `:w`
    - Save file
    - `:w <filename>` to "Save As"
  - `:wq` or `:x`
    - Save and exit
  - `:q!`
    - Exit without saving
  - `i`
    - Insert at current location
  - `I`
    - Insert at beginning of line
  - `a`
    - Append to end of word
  - `A`
    - Append to end of line
  - `dw`
    - delete word
  - `:d` or `dd`
    - delete line
  - `<#>G` or `:<#>`
    - Move to a particular line #

#### Can we work with multiple lines at the same time?

---

- Ranges
  - `:#,#<command>`
  - `:1,10d`
    - Deletes line 1-10
  - `:set number`
    - Displays line numbers
    - `:set number!` to disable
    - `vi +# filename` opens a file to a particular line
      - `vi +12 file.txt`
    - To be permanent
      1.  `vi ~/.vimrc`
      2.  `set number`

#### How would we perform a search in vi?

---

- Search
  - `/<string>` or `:s/<string>`
    - Search forward for text
    - `?` for backward
    - `n` for next
    - `N` for previous
  - `vi +/<text> filename.txt`
    - Opens a file to the first occurrence of a term

#### Does vi support search and replace as well?

---

- Search and Replace
  - `:s/<findtext>/<replacetext>`
    - Replaces text on one line
  - `:%s/<findtext>/<replacetext>`
    - Replaces text throughout the file
  - `:#,#s/<findtext>/<replacetext>`
    - Replaces text within a range

#### How can we navigate in vi if our terminal does not support arrow keys?

---

- `h`
  - Move left
- `l`
  - Move right
- `k`
  - Move up
- `j`
  - Move down
- `i`
  - Insert before cursor
- `o`
  - New line after line
- `a`
  - Append after cursor

#### What about options like cut/copy/paste?

---

- `d`
  - Delete
  - `dd` - delete line
  - `dw` - delete word
  - `D` - delete to the end of the line
  - `:d` - delete current line
- `y` (yank) - `yy` - Copy current line
- `p` (put)
  - `p` - Paste buffer after the current line

#### When we are done, how do we save and exit vi?

---

- `ZZ`
  - exit and save changes
- `:w!`
  - save overwriting file
- `:q!`
  - Exit ignoring any changes
- `:e`
  - switch to another file
- `:e!`
  - switch to another file without saving current file
