### Manipulating Text

#### Let's start simple, how can we get text on our screen?

---

- `echo`
  - `echo 'Hello world!'`
- `printf`
  - More control/options
  - `printf "Hello.\nWhat's your name?"`

#### What is an example of what we can do to the text?

---

- `wc`
  - `-c` Display the byte count.
  - `-m` Display the character count.
  - `-l` Display the newline count.
  - `-w` Display the word count.
  - `wc dracula.txt`

#### Can we actually change the text?

---

- `sort`
  - Changes sort order of text output
  - Relies on "columns" which require a delimiter of some sort
  - `-t` Delimiter
  - `-r` Reverse sort order (descending)
  - `-k` Column number
  - `sort -k 2 -t, ./cal-2019.txt`
- `cut`
  - Extracts a column of data from text
  - `-c` Character number to extract
  - `-f` Field number to extract
  - `-d` Delimiter
  - `cut -f 2 -d, ./cal-2019.txt`

#### If we've modified the file, is there a way to compare it to the original?

---

- `diff`
  - Compares contents of two files for differences
  - `-i` Ignore case differences.
  - `-w` Ignore spacing differences and tabs.
  - `-c` Display a list of differences with three lines of context.
  - `diff dracula.txt kermit.txt`

#### Are there more advanced tools available for text manipulation?

---

- `awk`
  - Matches strings within a set of data
  - Can be used to locate/delete text
  - Uses regular expressions
  - `awk '$1 == "Apache"' software_list.txt`
- `sed`
  - Stream Editor
  - `d` Delete the lines that match a specific pattern or line number.
  - `-n,p` Print only the lines that contain the pattern.
  - `s` Substitute the first occurrence of the string in the file.
  - `s,g` Globally substitute the original string with the replacement string for each occurrence in the file.
  - `sed '/Apache/d' software_list.txt`
