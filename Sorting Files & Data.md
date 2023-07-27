## Make some random data in Linux

### Generate 100 random numbers

`shuf -r -i 0-10000000000 -n 100 > numbers.txt`

### Generate 100 numbers with balues between 0 and 9, inclusive

`shuf -r -i 1-10 -n 100 > numbers0-9.txt`

### Generate 100 random words

```shell

# Script courtesy of https://linuxconfig.org/random-word-generator


if [ $# -ne 1 ]

then

echo "Please specify how many random words would you like to generate !" 1>&2

echo "example: ./random-word-generator 3" 1>&2

echo "This will generate 3 random words" 1>&2

exit 0

fi

# Constants

X=0

ALL_NON_RANDOM_WORDS=/usr/share/dict/words

# total number of non-random words available

non_random_words=`cat $ALL_NON_RANDOM_WORDS | wc -l`

# while loop to generate random words

# number of random generated words depends on supplied argument

while [ "$X" -lt "$1" ]

do

random_number=`od -N3 -An -i /dev/urandom |

awk -v f=0 -v r="$non_random_words" '{printf "%i\n", f + r * $1 / 16777216}'`

sed `echo $random_number`"q;d" $ALL_NON_RANDOM_WORDS

let "X = X + 1"

done


```

- You can sort tabular data using the -k option.
- you need to give the -k option a `KEYDEF`
- `3nr` means sort using column 3, and use the -n and -r options
- To sort `human-readable` data use the `-h` option not the `-n`(You cant use at the same time)
- You can sort by month by using the `-M`
- Order of option in the `KEYDEF` dont matter (as usual).
- The sort commands sorts "smallest first"

## How do we sort those words

`sort words.txt`
`sort words.txt > sorted.txt`

`sort words.txt | tac`
`sort -r words.txt`
`sort -r words.txt | less`

## Sorting numbers?

- sorts 0 - 9 by default.
  `sort -n numbers.txt`
- You can do this in reverse by adding the `-r` command
  `sort -nr numbers.txt | less`

## Show unique numbers not duplicates

`sort -u numbers[0-9].txt | less`

`ls -l /etc | head -n 20 | sort -k 5n`
`ls -hl /etc | head -n 20 | sort -k 5hr`

## Sort by month

`ls -hl /etc/ | head -n 20 | sort -k 6M`
`ls -lh /etc | head -n 20 | sort -k 6Mr`

`sudo find -maxdepth 4 -type f -size +1M -exec ls -lh {} \; | sort -k 5hr > ~/filesizes.tx`
