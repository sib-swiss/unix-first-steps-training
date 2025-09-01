# FAQ questions not clean-up and integrated yet

## Non-cleaned FAQs

### Question about an exercise

It worked with `ls -l *[ao]??x*_*[{i,ra}]`,  but [{i,ra}] worked by chance or
is it just redundant? (this is a question for additional tasks of exercise 2)

Answer: Actually this work by chance (so maybe I should change it !!), and the
reason is because the only species that ends with the letter “a” is
“Pteralopex_pulchra” (which ends in “ra”).

Here is why: actually what “*[ao]??x*_*[{i,ra}]” does, is that it will expand to:

ls -l *[ao]??x*_*[i] *[ao]??x*_*[ra]

And so it will match species names that either end with “i”, or that end with
“r” OR “a” (but not necessarily the pattern “ra”. As it happens, the only
species that ends in “a” is the one that ends in “ra”, which is why it works
in this case.
Note that in addition, is also happens that there are matches that end both
in “i” or “a”, otherwise the command would return an error saying one of the
matches did not work (well, actually this would also happen without the []
around the `{}` … if you want to avoid this problem here, you need to use
“pattern matching”, as shown in the solutions).

<br>
<br>

### Question about an exercise

Question: paste array_data_sorted-*.tsv
=> how do you know it will sequentially paste column1 of file1, column2 of
file 1, then column1 of file2 etc. and not mix everything up?
Do you need to see with “head” before to decide that your next “cut” will be
(for this case) cut -f 1,2,4,6 ?

Answer: “paste” will always paste the entire content (i.e. all columns) of a
file before pasting anything from the next file.
As for the order of files, the “filename expansion” mechanism will expand them
in alphabetical order, so first “array-1”, then “array-2”, then “array-3”.
So the oder is deterministic, and in principle, I could already know it without
having to use “head” to preview my result.

<br>
<br>

### About grep, what is the definition of “beginning” and “end” of a line ?

The “beginning” is the first character of the line, and “end” is the last
character of the line.
Thanks, so it’s only for character but not “patterns” as in repetitive or long
No, you can also use it for patterns, it just means that the patterns must
start from the start of the line, or be located at the end of the line.

E.g.  `grep "^red-panda"` selects all the lines that start with the text `red-panda`.
So `red-pandas are cute` would be selected, but not `a red-panda was here`.

<br>
<br>

### What is the difference between `chmod` and `sudo` ?

chmod  = change permission on files
sudo = run a command as “super user” (i.e. root).

Question: Can one actually limit the file permissions of the owner?
Yes sure, you can e.g. remove “w” rights, if you don’t want to overwrite a file
by mistake

```sh
chmod a-w <file name>  # this removes “write” permissions on the file (for everyone)
chmod a-x <file name>   # this removes “execution” permission on the file (for everyone).
```

<br>
<br>

### Is there a help page for searching unix commands/examples of usage of commands or a built-in help?

For most commands, you can use either `man command` or `command --help`.
For instance: `man cut`, `man paste` (detailed help) or `paste --help` (short version).

If you want a guide to all basic UNIX commands, you can see
<https://www.gnu.org/software/coreutils/manual/html_node/index.html#toc-Output-of-entire-files-1>
, but it’s long !

<br>
<br>

### Changing file permissions on Windows machines

J'ai testé sur un machine Windows et effectivement la commande "chmod" ne peut pas changer les permissions des fichiers sous windows car le système de permission de Windows est différent du système UNIX.

Si tu utilise WSL (windows subsystem for linux), il est possible de changer les permissions des fichiers crées dans ton "home" linux, mais pas sur la partition windows sous /mnt/c.
Pour quand-même avoir la possibilité de modifier les permissions des fichiers sur la partition windwows (typiquement le disque C sous /mnt/c), il est possible de procéder comme suit:

Executer dans le shell du WSL: sudo umount /mnt/c && sudo mount -t drvfs C: /mnt/c -o metadata
Les permissions des fichiers sous /mnt/c peuvent à présent être modifiés, mais attention, car les fichiers existant appartiennet maintenant au user "root", et donc ton user normal ne pourra les changer que avec "sudo chmod ...". Pour les fichiers nouvellement crées par ton user, les permissions pourront être changées sans avoir besoin du "sudo" ("sudo" est la command pour executer des commandes comme user "root" - i.e. admin/superuser).


Plus de détails sont donnés ici: <https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements>


<br>
<br>
<br>

## Supplementary tips for your interest (beyond the scope of this course):

### How to chain commands, i.e. run multiple commands in a single command line

Commands can be chained with the following operators:

* `;`: Commands are executed one after the other, regardless of the
  success/failure of the previous command.
  Example: echo "This is command 1"; echo "This is command 2"
* “&&”: The command after “&&” is executed only if the previous command succeeds.
  Example: echo "This is command 1" && echo "This is command 2"
* `||`: The command after “||” is executed only if the previous command fails.
  Example: echo "This is command 1" || echo "or that command 2"
