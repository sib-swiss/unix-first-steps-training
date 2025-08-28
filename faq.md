# Frequently asked questions

This is a list of questions that were asked during previous courses. You can
check it to see if your question is already answered.

:fire:
**Tip**: if you are viewing this document on GitHub, click on the "Outline"
(table of content) button (near the top-right side of the page) to show a list
of all questions.

<br>
<br>

## Environment setup

### Windows subsystem for linux (WSL): how can I navigate to the windows partition ?

If you are using WSL, the shell starts by default in the "home directory" of
WSL (which is different from your windows home directory). From there, you can
navigate to your windows `C` drive using the following command:

```sh
cd /mnt/c
```

*Note:* if your windows drive is not named `C` (but another letter), replace
`C` with the letter of your windows partition.

<br>
<br>

### How can I create, list or delete an alias ?

* To create a new alias: `alias alias_name='command to alias'`
* To list all existing aliases, simply type: `alias`
* To remove an alias you created: `unalias alias_name`

Examples

```sh
# Create
alias ll='ls -lh --group-directories-first --color=auto'

# Remove the "ll" alias
unalias ll
```

<br>
<br>
<br>

## File system navigation and display

### How can I find my current position in the filesystem ?

If you don’t know your position in the directory tree, you can type **`pwd`**
(for "print working directory"). This will print the path of your current
working directory.

Alternatively, if you know the absolute path of where you want to go, you can
`cd /absolute/path/to/your/dir`. In this way you don’t need to use the relative
path.

*Bonus*:
* Another command that can sometimes be useful is **`tree`**. It displays a
  visualization of the directory and file structure, by default starting from
  the position of your current working directory. If you want to see the
  structure of a specific directory, you can use `tree /path/to/dir`.
* Note that, on most systems, the `tree` command is not available by default
  and must be manually installed. See
  [this question](#how-to-install-the-tree-command-on-a-linuxmacos-system-) for
  how to install it.
* Warning: if you have a lot of directory/files, the `tree` output will be
  very long and it might therefore not be ideal.

<br>
<br>

### How can I go back to the previous working directory ?

To navigate back to the previous directory, the command is `cd -`.

<br>
<br>

### What are “hidden” files and how can I list them ?

By convention, file names starting with a `.` (dot), e.g. `.bashrc` are
hidden by the shell. This means that they are not displayed when you type `ls`
or `ls -l`.

To show/list these files, you have to add the `-a` option to the `ls` command,
as in the following example:

```sh
ls -a
```

<br>
<br>

### How can I sort files by time (`ls -t`), while also displaying the date associated with each file ?

This can be achieved by combining both the `-t` and `-l` options of `ls`.

```sh
ls -lt
```

<br>
<br>

### What is the meaning of colors in the output of the `ls` command ?

The color codes are system-dependent (and can be customized), but in most
cases, the meaning of the colors is the following:

* Blue = directories (folders)
* White = regular files
* Green = executable files
* Red = archive files (e.g. `.zip`)

<br>
<br>

### MacOS: how can I get files/directory colors the `ls` command on a Mac ?

On MacOS, you can get the colored output with `ls -G`.

If you want to create an alias for `ls -G`, you could do:

```sh
alias ls=”ls -G”

# Same, but additionally adding the -h option to the alias.
alias ls=”ls -h -G”
```

<br>
<br>

### When I execute `ls -l` I get my username written twice, in the 3rd and 4th column, why is that ?

```
-rw-r----- 1 alice alice 5.4K May 15  2015 ./funny_hamster.jpeg
-rw-r----- 1 alice alice 5.4K May 15  2015 ./cool_raccoon.png
```

The value in the 3rd column is the "owner" of the file, and the 4th column
shows the "group" of the file.

On most UNIX/Linux systems, a the user's username is also the name of their
default group. That’s why the user name appears listed twice (once as "owner"
and once as "group" name).

<br>
<br>

### What is the difference between the home directory and the root directory ?

The **home directory** is your personal space on the file system, and it is
typically the location where you can carry-out work, and where all your
personal files and configurations are stored.

* If multiple users share a machine (e.g. a compute server), then each user
  has their own "home" directory.
* The location of the home directory is os-dependent. On Linux machines, the
  home directory is typically located at `/home/<user name>`.
* Users have full read/write permissions inside their home directory.
* `~` and `$HOME` are shortcuts/variables that will expand to the user's home
  directory.
* running `cd` without any argument is shortcut for `cd ~` or `cd $HOME`.

The **root directory** (`/`) is the top-level directory of the entire
filesystem hierarchy, the "origin" of the filesystem. There is no parent
directory to the root directory, and it contains all files/directories present
on your machine.

* The path of the root directory is `/`.
* All other directories, such as `/home` or `/bin`, are contained inside of `/`.
* `cd /` will change into the root directory.
* Only the root user (administrator) has full access to modify everything
  under `/`. If you are logged-in as the root user, be careful when
  deleting/editing files outside of `/home`, as they might be critical
  operating system files.
* *Note:* the root directory (`/`) is not the same as the home directory of
  the root user (`/root`).

Some references to learn more about the linux directory structure:
* https://www.man7.org/linux/man-pages/man7/file-hierarchy.7.html
* https://linuxhandbook.com/linux-directory-structure

<br>
<br>
<br>

## File management and displaying file content

### What’s the difference between `mv file-1 file-2` and `cp file-1 file-2` ?

* `mv file-1 file-2` renames `file-1` into `file-2` (`file-1` no longer exists).
* `cp file-1 file-2` creates a copy of `file-1` named `file-2`.

<br>
<br>

### How can I display the “hidden” characters of a file, like tabs or newlines ?

One option is to use the **`-A`** option of `cat`: `cat -A <file name>`.
This will display tabs as `^I` and newlines as `$`.

Example: `cat -A test_file.md` will print the following.

```txt
# A test file to display hidden characters$
$
Here is a simple space: $
Here is a tab:^I$
Here are 2 tabs:^I^I$
$
```

If the file is very large and we don't want to print it all at once, we can
pipe the output of `cat` into `less`: `cat -A test_file.md | less`.

Alternatively, we can also use `od -c test_file.md`, that will print tabs as
`\t` and newlines as `\n`.

```txt
0000000   #       A       t   e   s   t       f   i   l   e       t   o
0000020       d   i   s   p   l   a   y       h   i   d   d   e   n    
0000040   c   h   a   r   a   c   t   e   r   s  \n  \n   H   e   r   e
0000060       i   s       a       s   i   m   p   l   e       s   p   a
0000100   c   e   :      \n   H   e   r   e       i   s       a       t
0000120   a   b   :  \t  \n   H   e   r   e       a   r   e       2    
0000140   t   a   b   s   :  \t  \t  \n  \n  \n
0000152
```

<br>
<br>
<br>

## Using and installing commands (programs)

### How to exit the `man` program when looking-up a UNIX command ?

To exit the `man` program, simply type on the `q` key of your keyboard.

*Bonus:*
* To perform a search in the text displayed by man, you can use
  `/search_term + Enter` (replace `search_term` by the term you are looking
  for, e.g. `/-t` if you are looking for the `-t` option in the manual.
* You can jump to the next/previous match by typing `n` or `N` on your
  keyboard.

<br>
<br>

### I can get help using `man` for commands `ls` and `pwd`, but not for `cd`. Why is that ?

The reason is that `cd` is a **shell built-in command**, it is part of the
shell itself. `ls` and `pwd` on the other hand are "regular" commands, i.e.
they are separate executable programs located in directories like `/bin` or
`/usr/bin`.

To display the help for `cd` (or other built-in commands), you must use
`help cd`.

<br>
<br>

### How to install the `tree` command on a Linux/MacOS system ?

The `tree` command displays a visual representation of file/directory structure.
This command can sometimes be useful, but it's not essential to have it for
this course.

Here is how you can install `tree`:

* **MacOS**: The `tree` command is not available “out-of-the-box” for Mac.
  To install it, you can use [`brew`](https://brew.sh), a package manager for Mac
  that allows to install additional software. So you will first have to install
  [`brew`](https://brew.sh), and then you can install `tree` using the command
  `brew install tree`.
* **Ubuntu** (and other Debian Linux): `sudo apt-get install tree`

<br>
<br>

### How can I list processes running in the background and check their status?

To list all jobs that are currently running the background, use the command:

```sh
jobs -l`.
```

Here is an example:

```sh
sleep 60 &    # the “sleep 60” command will do nothing for 60 seconds, then exit.
jobs -l       # This will show: [1]+ 199704 Running             	sleep 60 &
```

<br>
<br>
<br>

## Compressing and archiving data

### Why is `-z` needed to decompress a `.tar.gz` file with the `tar` command ?

By default **TAR files** are not compressed, they are just a “bundle of files”.
Historically, the TAR format was created to facilitate the writing of files to
magnetic tapes (hence the name **T**ape **AR**chive).

This is why the `tar` command does not compress/decompress data by default, and
the `-z` option must be passed to compress/decompress data.

*Note:* technically `tar` is not able to compress/decompress data itself.
Instead, if you pass it it the `-z` flag, it will *invoke* an compression
command (in this case `gzip`) to do the work of compressing/decompressing data.

<br>
<br>
<br>

## Questions related to exercises

### To concatenate 2 files and then delete them, would `cat file1 file2 > file3 | rm file1 file2` work ?

The **`|` (pipe) operator** passes the standard output of one command as the
standard input of another command. Here we don’t really want to pass any
content between the two commands `cat` and `rm`. Instead we just want to
execute the second command **if** the first one was successful.

For this we use the `&&` operator to chain commands:

```sh
cat file1 file2 > file3 && rm file1 file2
```

This would first concatenate the two files, then (if the `cat` command
succeeds), the `rm` command would be executed, and `file1` and `file2` would
be deleted.

*Note:* we can also use **`||`** to execute a second command **if** the first
one fails.


<br>
<br>

### Why does `find . -name '*.jpeg' -or '*.png'` not work ?

You must repeat the **`-name`** instruction in the part that is located after
the `-or` operator:

```sh
find . -name '*.jpeg' -or -name '*.png'
```

<br>
<br>
