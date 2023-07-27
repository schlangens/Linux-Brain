- Changes all of the txt documents in current working directory to csv files
  `ren "*.txt*" "#1.csv"`

- Prefix my-file to all csv files in working directory
  `ren "*.csv" "my-#1.csv"`

- You concat files with "CAT/TYPE"
  `type my-file1.csv my-file2.csv > newfile.txt`
  `cat my-file1.csv my-file2.csv > newfile.txt`
  `cat my-file*.csv > final-file.csv`

- Append content
  `type my-file2.csv >> my-file1.csv`
- Add date
- Displays Year-Month-Day format
  `date +"%Y-%m-%d"`
  `ren "my-file*.csv" "my-file#1- 'date "+%Y%m%d"'"`
