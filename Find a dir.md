In Linux, you create multiple files and directories and frequently navigate in between but there are times when the number of directories is so huge that finding it is next to impossible.

So what options do you have in that case?

You can [use the find command](https://linuxhandbook.com/find-command-examples/)[[1]](https://linuxhandbook.com/find-directory/#readabilityFootnoteLink-1) with multiple parameters to look for that specific directory hidden in the heavens. Use `-type d` to indicate that you are specifically looking for directories, not files.

Let me show you how.

## 1. Find a directory using its name

By far, this is the most common and simple way to search for a directory where you know the name of the directory and where to find it and that's it!

To find directories using their names, you can use the find command in the following manner:

```
find /path/to/search -type d -name directory_name
```

Here,

- `/path/to/search` is where you will give the path of the directory where you want to initiate the search.
- `type -d` indicates you want to search for the directories only.
- `-name` indicates you want to indicate the name search.
- `directory_name` is where you enter the name of the directory which you want to search.

Let's suppose you want to search for a directory named `Downloads` in the home directory, then, I will be using the following:

```
find ~/ -type d -name "Downloads"
```

![search directory using the name in Linux](https://linuxhandbook.com/content/images/2023/07/search-directory-using-the-name-in-Linux.png)

## 2. Find a directory modified on a specific date

If you want to list the directories that were modified on a specific date, then, you can use the find command in the following manner:

```
find /path/to/search -type d -newermt "YYYY-MM-DD" ! -newermt "YYYY-MM-DD"
```

Here, the `-newermt` flag was used two times. **One to specify the lower limit** and another **one was used for the upper limit** indicating on that date or before that.

By doing so, you create a time frame of two dates.

For example, if I want to list all the directories modified between the 16th and 18th of Jul 2023, then, I will be using the following:

![](https://linuxhandbook.com/content/images/2023/07/find-directories-based-on-their-modification-date-using-the-find-command-in-Linux.png)

## 3. Find directories modified in the last n days

To look for directories that were modified in the last n days, you can use the `-mtime` flag with the find command:

```
find /path/to/search -type d -mtime -days
```

So if I want to find directories modified in the last 7 days, then, I will be using the following:

```
find ~/Test/ -type d -mtime -7
```

![find directories modified in the last n days in Linux](https://linuxhandbook.com/content/images/2023/07/find-directories-modified-in-the-last-n-days-in-Linux.png)

## 4. Find a directory modified more than N days ago

Similar to the above, if you want to find directories that were modified in more than N days ago, then you'd have to use the `-mtime` command in the following manner:

```
find /path/to/search -type d -mtime +days
```

For example, if I want to find directories that were modified more than 7 days ago, then, I will be using the following:

```
find ~/Test/ -type d -mtime +7
```

![find directories modified N days ago](https://linuxhandbook.com/content/images/2023/07/find-directories-modified-N-days-ago.png)

## 5. Find empty directories

To [find empty directories](https://linuxhandbook.com/find-empty-directories/)[[2]](https://linuxhandbook.com/find-directory/#readabilityFootnoteLink-2), all you have to do is use the `-empty` flag as shown:

```
find /path/to/search -type d -empty
```

Let's say I want to find empty directories inside the `Test` directory, then, I will be using the following:

```
find ~/Test/ -type d -empty
```

![find empty directories in Linux](https://linuxhandbook.com/content/images/2023/07/find-empty-directories-in-Linux.png)

## Here's how to check the size of a directory

If you're curious to know how to check the size of the directory, then, you can follow our detailed guide on [how to check the size of the directory](https://linuxhandbook.com/find-directory-size-du-command/)[[3]](https://linuxhandbook.com/find-directory/#readabilityFootnoteLink-3):

[

How to Check Directory Size in Linux Command Line

The du command in Linux is used for checking the size of directory. Here are various ways you can find the size of directory in Linux with the du command.

![](https://linuxhandbook.com/content/images/2020/06/du-command-linux-featured.png)

](https://linuxhandbook.com/find-directory-size-du-command/)[[4]](https://linuxhandbook.com/find-directory/#readabilityFootnoteLink-4)

I hope you will find this guide helpful.

### References

1. [^](https://linuxhandbook.com/find-directory/#readabilityLink-1 "Jump to Link in Article") [use the find command](https://linuxhandbook.com/find-command-examples/) (linuxhandbook.com)
2. [^](https://linuxhandbook.com/find-directory/#readabilityLink-2 "Jump to Link in Article") [find empty directories](https://linuxhandbook.com/find-empty-directories/) (linuxhandbook.com)
3. [^](https://linuxhandbook.com/find-directory/#readabilityLink-3 "Jump to Link in Article") [how to check the size of the directory](https://linuxhandbook.com/find-directory-size-du-command/) (linuxhandbook.com)
4. [^](https://linuxhandbook.com/find-directory/#readabilityLink-4 "Jump to Link in Article") [How to Check Directory Size in Linux Command Line The du command in Linux is used for checking the size of directory. Here are various ways you can find the size of directory in Linux with the du command.](https://linuxhandbook.com/find-directory-size-du-command/) (linuxhandbook.com)