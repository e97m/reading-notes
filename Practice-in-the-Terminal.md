# Practice in the Terminal

![Bash](./imgs/bash.png)

<br>

## The Command Line

 Bash is the most common shell for the Linux command line or terminal (text-based interface to the system). command line may seem daunting, complex and scary. But it is actually quite simple and intuitive once it's well understood. The command line is an interesting beast, so it's worth it.

 ### Relevent commands 

 - `echo` : To check what shell do you use.

 <br>

## Basic Navigation

A lot of commands on the terminal will rely on you being in the right location. As you're moving around, it can be easy to lose track of where you are at. so, it's important to navigate smoothly.

Absolute paths specify the location of a file or directory in relation to the root directory. It begins with `/`. Relative paths specify the location in relation to where we currently are in the system. They won't begin with a slash.

### Relevent commands 

- `pwd` : Print Working Directory, tells you what your current or present working directory is
- `ls` : List, to show what is inside the current directory. you can add options to `ls` such as:

     - `-l` :  Long listing, to show details about files and folders.
     - Any directory name : list that directories contents
     - `/etc` : Show config files for the system
     - `/var/log` : Sow log files for various system programs.
     - `/bin` or `/usr/bin` : Show the location of several commonly used programs.

- `~ ` : Home directory.
- `.` : Current directory.
- `..` : Parent directory.
- `cd` : Change directory, you should type the location as a path after it, otherwise it will take you to home.

<br>

## More About Files

Everything in Linux is actually a file. A text file is a file under the hood, a directory is a file, your keyboard is a file (one that the system reads from only), your monitor is a file (one that the system writes to only), etc. It is good to mention that Linux is case-sensitive when it comes to files names, paths, command lines... etc. 

Spaces are fine in Linux but when you need to insert the file name as an option to a command you have to put it inside quotations or use the escape character (\) before the space.

Hedden files in Linux are the ones that ints name starts with (.), configuration files is a good example for hidden files.

### Relevent commands 

- `file` + file-path or file-name : shaows the type of file
- `ls -a` : Show hidden files

<br>

## Manual Pages

The manual pages are a set of pages that explain every command available on your system including what they do. To search within a manual page press forward slash `/` followed by the term you would like to search for and hit 'enter' If the term appears multiple times you may cycle through them by pressing the `n` button for next.

### Relevent commands 

- `man [command to look up]` : Show the manula of a commad
- `man -k [search term]` : Search for manual by a term inside it.

<br>

## File Manipulation

Linux organizes its file system in a hierarchical way. It's helpful and time-saving to use the feature of directories for organizing the files. But be careful, the Linux command line does not have an undo feature. Perform destructive actions carefully.

### Relevent commands 
- `mkdir` + directory-path or directory-name : Make a new directory.
    - `-p` : Make parent directory
    - `-v` : Write on the screen what it the command doing.
- `rmdir` + directory-path or directory-name : Remove an empty directory
- `touch` + file-name : Create a blank file
- `cp` + source + destination : Copy.
    - `-r` : copy directory and recursive files (all files and directories within it, and for subdirectories).
- `mv` + source + destination : Move and rename.
- `rm` : remove file.
    - `i` : interactive, prompt you before removing and give you the option to cancel the command.
- `rm -r` : remove directory (recursive).

<br>

# Finally, have a look at Linux command [Cheat Sheet](https://ryanstutorials.net/linuxtutorial/cheatsheet.php)