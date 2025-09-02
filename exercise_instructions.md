# Exercises - Introduction to Linux / UNIX and the Bash shell

<br>

## Before you start

* :pencil:
  **Exercise material setup:** download the
  [exercises.zip](https://github.com/sib-swiss/unix-first-steps-training/raw/main/exercises.zip)
  archive file to your local computer and unzip it. This will unpack a
  directory named `exercises`, with all the data needed for the course
  exercises.

* :pencil2:
  **Additional Tasks:** at the end of each exercise, you will find a section
  named **Additional Tasks**. These sections contain tasks to complete
  **if you have the time and after having completed the main exercise**.
  Additional tasks sections will not be corrected in class, but their solution
  is given in this document.

* :white_check_mark:
  **Exercise solutions:** all exercises and additional tasks section have
  their solution embedded in this document. Solutions are hidden by default,
  but you can reveal them by clicking on them. Here is an example:

  <details><summary><b>Exercise solution (click to reveal)</b></summary>
  :sparkles: This reveals the answer :sparkles:
  </details>

  We encourage you to **not look at the solutions too quickly**, and try to
  solve the exercises without them. Remember that you can always ask the
  course teachers for help.

* :fire:
  **Tip:** if you are viewing these instructions on the GitHub web-interface,
  you can display a table of content (outline) of this page by clicking on the
  small icon that looks like a bulleted list near the top-right of this page.

* :shell:
  The exercises instructions are designed to work with the **bash** shell,
  but should also work in other shells, such as the **zsh** shell that is
  found by default on MacOS. To find out what shell you are currently using,
  you can run the following command in your terminal:
  
   ```sh
   echo $0
   ```

  On MacOS, if you are in `zsh` and would like to **switch to `bash`**, you can
  simply type `bash`.

<br>
<br>
<br>

## Exercise 1 - Navigating the filesystem in command line [~20 min]

:triangular_flag_on_post:
**Objective:** get familiar with navigating the directory tree and listing
the content of directories.

<br>

Open a new terminal (shell) and perform the following tasks:

1. **Print the path of your current working directory** with the `pwd` command.
   This will show you where you are currently located in the directory tree.

2. **Navigate to the course's `exercises/` directory** (the one you unpacked
   from the `.zip` archive file), then enter the `exercise_1/` subdirectory.
   To make sure you are at the right location, use the `pwd` command again.

   <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     # The actual location of the "exercises" directory depends on where you
     # unzipped it on your system.
     cd /path/to/directory/exercises
     ls -l
     cd exercise_1
     pwd
     ```

    :sparkles: changing directory to `exercise_1` can of course also be done
    in a single command:

     ```sh
     cd /path/to/directory/exercises/exercise_1
     pwd
     ```

   <br>
   </details>

3. **List the content** of the `exercise_1/` directory with `ls`, `ls -l`,
   `ls -lh`, and `ls -lha`.
   * :question:
     **Question:** what do the `-l`, `-h` and `-a` options do?
   * :dart:
     **Hint:** you can use `man ls` to display the help for the `ls` command.
     To exit the help, simply type `q` on your keyboard.
   * :sparkles:
     **Notes:**
     * One-letter options can be grouped together, so `ls -lha` is the
       same as `ls -l -h -a`.
     * Some options have both a "short" and a "long" form. E.g. `ls -lah`
       is the short form for `ls -l --all --human-readable`.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls       # Prints the names of files and directories.

    ls -l    # List content of the subdirectory in "long listing" format. This
             # provides additional details for each file/directory, such as
             # its permissions, its size and its last modification date.

    ls -lh   # Adding the "-h" option displays file sizes in "human readable"
             # format. The size of files are shown in kB, MB, GB, instead of
             # their size in bytes (octets).

    ls -lha  # Adding the "-a" option additionally displays hidden files and
             # directories. These are files/directories whose name starts with
             # a dot ".".
             # Hidden files are often used to store program configurations.
    ```

   <br>
   </details>

4. **List the content of the directory in chronological order** (newest file
   first) and in reverse chronological order (oldest file first).

   * :dart:
     **Hint:** the option to sort by time is `-t`. To reverse sorting use
     `-r`/`--reverse`.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls -lht    # The "-t" option sorts by time, newest file first.
    ls -lhtr   # Adding the "-r" option reverses the order of sorting
               # (oldest file first).
    ```

    Some other useful `ls` options:

    ```sh
    ls -a/--all  # Also show hidden files.
    ls -R        # --recursive, list subdirectories recursively.
    ```

    <br>
    </details>

5. A very handy functionality that bash (and other shells) provides is
   the ability to **auto-complete file/directory names**. Simply start typing
   the name of a file/directory, and then press on **Tab** on your keyboard:

   * The shell will autocomplete (as much as possible) the file/directory name.
   * If there are multiple matches for the characters you started to type, the
     shell will stop the auto-completion at the point where the names diverge.
   * To continue auto-completion, your need to type additional characters that
     allow the shell to disambiguate between the different matches, and then
     press **Tab** again. You can also press **Tab** again to display
     all the possible matches at this point.

   Try this functionality by auto-completing the name of the file
   `a_regular_file_with_a_really_long_name.md` (found in the `exercise_1`
   directory):

   * Start by typing `ls a`, then press on **Tab**. You will see that the
     shell auto-completes up to `ls a_`.
   * Double-press on the **Tab** key to display all possible matches at this
     point. You should see 3 values: `a_directory/`, `a_regular_file.txt` and
     `a_regular_file_with_a_really_long_name.md`.
   * To disambiguate between the 3 possible matches, enter the additional
     character `r` and press on **Tab** again. The shell should should now
     auto-complete up  to `ls a_regular_file`.
   * At this point there are 2 possible matches left: `a_regular_file.txt` and
     `a_regular_file_with_a_really_long_name.md`. To disambiguate between them,
     enter the additional character `_` and then press on **Tab** again.
   * The full name of the file `a_regular_file_with_a_really_long_name.md`
     should now have auto-completed, and you should have the following
     command ready to be run:

     ```sh
     ls a_regular_file_with_a_really_long_name.md
     ```

   * You can now press the **Enter** key on your keyboard to run the `ls`
     command with the auto-completed file name.

6. In the current working directory, **run the command `cd .`** - you should
   observe that this command has **no net effect** (i.e. it did not change
   directory).
   * :question:
     **Question:** what is the meaning of **`.`** in the command **`cd .`** ?

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    **`.`** is the **relative path of the current directory**. Therefore,
    running `cd .` has no effect as it simply changes to the same directory
    we are already in.

    The `.` shortcut is useful in some situations. E.g. if you want to copy
    a file to the current directory you can do `cp /file/to/copy .`, or you
    can run an executable located in the current directory with `./run_me.sh`.

    <br>
    </details>

7. **Change your working directory** to the `exercise_2/` directory using its
   **relative path**. `exercise_2/` is located in the same parent directory
   as `exercise_1`, your current working directory.
    * :dart:
      **Hint:** the relative path of the parent directory is **`..`**

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     cd ../exercise_2/
     ```

    **`..`** is the **relative path of the parent directory**. Multiple levels
    of `..` can be combined to go up multiple levels. E.g. `cd ../..` will go
    up two levels in the directory tree.

    Here are is a summary of useful `cd` shortcuts:

     ```sh
     cd .         # Does nothing, we stay in the same directory.
     cd ..        # Go to parent directory.
     cd /         # Go to root directory.
     cd ~         # Go to user's home directory, on Linux: /home/<user name>.
     cd -         # Go back to the previous directory.
     cd           # With no argument, cd brings you back to your home directory.
     ```

    <br>
    </details>

<br>

### Additional Tasks 1

8. **Try the `cd ~` and `cd -` shortcuts**. What do they do?

   <details><summary><b>:white_check_mark: Solution</b></summary>

    * **`~`** is a shortcut for the "home directory", and therefore `cd ~` is a
      shortcut to change directory to your home directory.
    * **`-`** is a shortcut to change to the previous working directory. It is
      handy if you want to return to a directory you were in just previously.

   <br>
   </details>

9. **Create an alias named `ll`** that runs the following command:
   `ls -lh --group-directories-first --color=auto`.

   :sparkles:
   **Notes:**
   * On some Linux system, an `ll` alias may already exist.
   * To list your currently defined aliases, you can type `alias` to list them
     all, or `alias <name of alias>` to list a specific one (e.g. `alias ll`).
   * Aliases only live as long as your current shell session. To make aliases
     permanent, they must be defined inside a **configuration file**, such as
     **`~/.bashrc`**, so that they get loaded each time a new shell is spawned.
   * To remove an alias from the current shell, use `unalias <alias name>`.
   * To remove a permanent alias, remove it from the config file
     (e.g. `.bashrc`) where it is defined.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     # Create a new "ll" alias:
     alias ll='ls -lh --group-directories-first --color=auto'
     ```

    Here are some some more useful commands for aliases:

     ```sh
     alias       # Lists the currently defined aliases.
     unalias ll  # Removes an alias - here "ll" - from the current shell session.

     # The "type" command tells if a command is an alias:
     #  * If yes, the aliased command is shown.
     #  * If not, the path to the binary file is shown.
     type ll    # -> ll is aliased to `ls -lh --group-directories-first --color=auto'
     type bash  # -> bash is /usr/bin/bash
     ```

   <br>
   </details>

10. **Compute the size of a directory**. To display the size of a directory,
    the command **`du -sh <directory>`** can be used. Try in on the directories
    found in `exercise_1`.

    <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     du -sh a_directory  # 20K  (20 kilobytes)
     du -sh b_directory  # 4K   (directory is empty, 4K is the size of an empty dir)

     # Using the ? wildcard character, we can also compute the size of both
     # directories in a single command.
     du -sh ?_directory
     ```

    <br>
    </details>

11. Let's look at a detail of **how the bash shell displays file sizes**.

    Go into the directory `a_directory` and list its content using the
    following commands - look at how file size is indicated:
    * **`**ls -l`**: lists the file size in **bytes/octets**.
    * **`ls -lh`** (you can also use your new `ll` alias!): the **`-h`** option
      (the short form of `--human-readable`) lists the file size in a more
      readable format, using the `k`, `M`, `G`, ... unit abbreviations for
      `kB` (kilobyte), `MB` (megabyte), `GB`, (gigabyte) etc.

    :sparkles:
    **Note:** in everyday language, the term **kilobyte** (abbreviated `kB`) is
    used for talking interchangeably about either 1000 bytes or 1024 bytes,
    because they represent almost the same quantity of bytes.  
    If we really wanted to be precise, the proper name for a unit of 1024 bytes
    is a *kibibyte* `KiB`, while a *kilobyte* designates 1000 bytes. Similarly,
    a *megabyte* is 1'000'0000 bytes, and a *mebibyte* is 1024^2 bytes (same
    with *gigabyte* vs. *gibibytes*, *terabyte* vs.*tebibyte*, etc.).

<br>
<br>
<br>

## Exercise 2 - Filename expansion with wildcard characters [~20 min]

:triangular_flag_on_post:
**Objective:** learn to use **filename expansion (globbing)** using
**wildcard characters** to match existing file names.

:sparkles:
**Notes:**

* The correct technical term for the expansion of wildcards characters by the
  shell is
  **[filename expansion](https://www.gnu.org/software/bash/manual/bash.html#Filename-Expansion)**,
  but it is often referred to as **globbing**.
* Globbing only matches **existing file/directory names**: expansion will not
  happen if there is no matching file/directory. This is why it's official
  name is *filename expansion*.
* :fire:
  **Tip:** If you don't want a specific wildcard character to expand
  (e.g. to list a file named exactly `test_*.md`.), you can:
  * **Quote it** (single or double quote): `ls "test_*.md"` or `ls 'test_*'.md`
  * **Escape it** by prefixing it with **`\`**: `ls test_\*.md`

<br>

To start this exercise, enter the directory `exercise_2/RedList_mammals` and
list its content with the command **`ls`**. You will see that it contains a
large number of files, whose names are those of the
**critically endangered mammal species** as listed in the
[International Union for Conservation of Nature (IUCN) Red List](https://www.iucnredlist.org).

The species names are given in
[binomial nomenclature (i.e. latin names)](https://en.wikipedia.org/wiki/Binomial_nomenclature),
and each file has the structure `Genus_species`. E.g. if there a was file for
humans, it would be named `Homo_sapiens`.

Using `ls` and wildcard characters, perform the following tasks:

1. **List all files starting with the letter `i`** (upper or lower case).  
   :dart:
   **Hint:** you should have 1 match.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    cd exercise_2/RedList_mammals/
    ls -l I*   # Returns a single match: Indri_indri (a lemur species).
    ```

    :sparkles:
    **Notes:**
    * In this exercise, since all file names start with a capital letter,
      `ls -l I*` is sufficient to list all files starting with the letter `i`.
      If there were also files starting with lower case letters, we would need
      to use `ls -l [iI]*`.
    * :warning:
      **`ls -l [iI]*`** and **`ls -l i* I*`** are not equivalent expressions:
      `ls -l i* I*` will return an error unless there exists *both* files
      starting with `i` and with `I` (you can test it in your terminal).

   <br>
   </details>

2. **List the files of [Rhinoceros species](https://en.wikipedia.org/wiki/Rhinoceros#Species)**
   (genus *Rhinoceros*, *Dicerorhinus*, and *Diceros*).  
   :dart:
   **Hint:** you should have 3 matches.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls -l Rhinoceros_* Dicerorhinus_* Diceros_*
    ls -l Rhinoceros* Dicero*                     # Gives the same result.

    # Dicerorhinus_sumatrensis  (Sumatran Rhinoceros).
    # Diceros_bicornis          (Black Rhino).
    # Rhinoceros_sondaicus      (Javan Rhinoceros).
    ```

    :sparkles:
    **Notes:**
    * Since both the genus `Dicerorhinus` and `Diceros` start with `Dicero`,
      we can match the pattern `Dicero*` to get both genuses at the same time.
    * :rhinoceros:
      There exists 2 other Rhino species:
      * The White Rhino (*Ceratotherium simum*) is
        [listed as "Near Threatened" by the IUCN](https://www.iucnredlist.org/species/4185/45813880).
        This species has two subspecies: the Northern and Southern White Rhino.
        The [Northern White Rhino](https://en.wikipedia.org/wiki/Northern_white_rhinoceros)
        is critically endangered with only 2 female individuals remaining
        worldwide (living in semi-captivity in Kenya).
      * The Greater One-Horned Rhino (a.k.a. Indian Rhino), *Rhinoceros unicornis*
        is [listed as "Vulnerable" by the IUCN](https://www.iucnredlist.org/species/19496/18494149).

   <br>
   </details>

3. **List the files of Gibbon species** from the genus
   *[Nomascus](https://en.wikipedia.org/wiki/Nomascus)* whose species
   name ends with either `r` or `i`.  
   :dart:
   **Hint:** you should have 2 matches.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls -l Nomascus_*[ri]

    # Nomascus_concolor  (Black crested gibbon).
    # Nomascus_siki      (Southern white-cheeked gibbon).
    ```

    :sparkles:
    **Note:** in this specific case, using `ls -l Nomascus_*[ri]` or
    `ls -l Nomascus*[ri]` gives the same result, but in principle the former is
    safer to use because it will only match genus names corresponding to
    exactly `Nomascus`, while the later could match any genus name starting
    with `Nomascus`.

   <br>
   </details>

4. **List the files of species that meet *both* of the following conditions**:
   * The genus name contains the pattern "`l` + a single letter + a letter
     between `a` and `h`", e.g. `lia` or `lug`.
   * The species name starts with a `g`.

   For instance, *Eubalaena glacialis*, the
   [North Atlantic right whale](https://en.wikipedia.org/wiki/North_Atlantic_right_whale),
   would be a match, because its genus name *Eubalaena* contains the pattern
   `lae` and its species name *glacialis* starts with a `g`.

   :dart:
   **Hint:** you should have 3 matches.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls -l *l?[a-h]*_g*

    # Eubalaena_glacialis    (North Atlantic right whale).
    # Gorilla_gorilla        (Western gorilla).
    # Plecturocebus_grovesi  (Alta Floresta titi monkey - a new world monkey)
    ```

   <br>
   </details>

<br>

### Additional Tasks 2

5. **List the files of species that satisfy both of the following conditions**:
   * The genus name contains the pattern "`a` or `o`, followed by exactly 2
     letters, followed by the letter `x`" (e.g. `abix` or `onyx`)
   * The species name ends either with an `i` or with the pattern `ra`.

   For instance, *Pteralopex pulchra*, the
   [Montane monkey-faced bat](https://en.wikipedia.org/wiki/Montane_monkey-faced_bat),
   would be a match, because its genus name *Pteralopex* contains the pattern
   `opex` and its species name *pulchra* ends with the pattern `ra`.

   :dart:
   **Hints:**
   * This pattern cannot be matched in a single expression using only regular
     file globbing (i.e. filename expansion). You will need to either:
     * Use 2 expressions with regular globbing.
     * Use [brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion).
     * Use [pattern matching](https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching).
   * You should have 4 matches.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    ls -l *[ao]??x_*[ra] *[ao]??x_*i  # Solution using pure globbing. Requires some duplication.
    ls -l *[ao]??x_*@(ra|i)           # Solution using pattern matching.
    ls -l *[ao]??x_*{ra,i}            # Solution using both globbing and brace expansion.

    # Myosorex_eisentrauti  (Eisentraut's mouse shrew).
    # Pteralopex_flanneryi  (Greater monkey-faced bat).
    # Pteralopex_pulchra    (Montane monkey-faced bat).
    # Sorex_sclateri        (Sclater's shrew).
    ```

    :sparkles:
    **Note:** to avoid duplicating the `*[ao]??x_*` part, we can use either
    **pattern matching** or **brace expansion**:
    * **[Pattern matching](https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching)**:
      here **`@(ra|i)`** matches either the pattern `ra` or `i`.
    * **[Brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion)**:
      during the shell's processing, braces `{}` are expanded first (before
      globbing), and therefore:

      ```sh
      ls -l *[ao]??x_*{[ra],i}
      ```

      is expanded into:

      ```sh
      ls -l *[ao]??x_*[ra] *[ao]??x_*i
      ```

      before file expansion (globbing) is performed.

   <br>
   </details>

6. **Try to add quotes (single or double) around a globbing pattern** with
   wildcards, e.g. `ls -l "I*"`.

   * :question:
     **Question:** what difference do the quote make (if any)?
   * :question:
     **Question:** can you think of a use case for using quotes around a
     pattern with wildcards?

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    Adding single or double quotes around the search pattern prevents the
    shell from performing file expansion (globbing). Instead, it will try to
    literally match the pattern. E.g. `ls -l I*` in the example below will try
    to find a file named `I*`, instead of any file starting with the letter `I`.

     ```sh
     ls -l 'I*'
     # ls: cannot access 'I*': No such file or directory
     ```

    One use case for adding quotes is if we e.g. want to store the pattern
    to match as a shell variable (e.g. in a shell script):

     ```sh
     # We store the pattern "I*" in a variable named "search_pattern".
     search_pattern="I*"
     echo ${search_pattern}

     # Later we can use our stored pattern to match files:
     ls -l ${search_pattern}
     # -> lists all files starting with "I".
     ```

    In this case, if we did not use quotes around `"I*"` when creating our
    `search_pattern` variable, file globbing would have occurred and the value
    of the variable would have been set to the file(s) name that match the
    globbing pattern, and not the pattern itself.

     ```sh
     search_pattern=I*
     echo ${search_pattern}  # The value of `search_pattern` is set to "Indri_indri"
                             # instead of "I*"... not what we wanted.
     ```

   <br>
   </details>

<br>
<br>
<br>

## Exercise 3 - File management: create, copy, move, and delete [~20 min]

:triangular_flag_on_post:
**Objective:** learn to use the commands to create, move, copy and delete files
and directories: **`mkdir`**, **`cp`**, **`mv`**, **`rmdir`**, **`rm`**.

<br>

Enter the directory `exercise_3/` and perform the following tasks:

1. **Create directories** with the **`mkdir`** command:
   * In the directory `exercise_3/`, create 2 new directories:
     `species_by_genus` and `species_by_common_name`.
   * In `species_by_genus/`, create 2 new sub-directories:
     `Dendrolagus` ([tree-kangaroos](https://en.wikipedia.org/wiki/Tree-kangaroo))
     and
     `Crocidura` ([a genus of shrews](https://en.wikipedia.org/wiki/Crocidura)).
   * In `species_by_common_name/`, create 2 new sub-directories
     named `B`, and `R`.

   :fire:
   **Tip:** to avoid having to rewrite a command, remember that you can use
   the **up arrow** of your keyboard to go back in your terminal history.
   This allows you to re-use a command that you wrote earlier, while making
   changes to it if needed.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    * **Create the directories `species_by_genus` and `species_by_common_name`**.

     ```sh
     cd exercise_3

     # Option 1: create one directory after the other.
     mkdir species_by_genus
     mkdir species_by_common_name

     # Option 2: create both directories with a single command.
     mkdir species_by_genus species_by_common_name

     # Option 3: use brace expansion to avoid repeating the common part of the directory names.
     mkdir species_by_{genus,common_name}
     ```

    * **Create sub-directories `Dendrolagus` and `Crocidura`**.

     ```sh
     # Option 1: create the sub-directories from the root of exercise_3.
     mkdir species_by_genus/Dendrolagus species_by_genus/Crocidura

     # Option 2: enter the "species_by_genus" directory, then create the sub-directories.
     cd species_by_genus/
     mkdir Dendrolagus Crocidura
     cd ..

     # Option 3: same as option 1, but using brace expansion to avoid repetition.
     mkdir species_by_genus/{Dendrolagus,Crocidura}
     ```

    * **Create sub-directories `B` and `R`**.

     ```sh
     mkdir species_by_common_name/B species_by_common_name/R

     # Option 2: enter "species_by_common_name", then create the sub-directories.
     cd species_by_common_name
     mkdir B R
     cd ..

     # Option 3: using brace expansions.
     mkdir species_by_common_name/{B,R}
     ```

    :sparkles:
    **Note:** using the **`-p` option of `mkdir`**, it is possible to create
    multiple levels of directories in a single command. For example, we could
    create all the directories for this exercise in a single command:

      ```sh
      mkdir -p species_by_{genus/{Dendrolagus,Crocidura},common_name/{B,R}}
      ```

    :fire:
    **Tip:** to preview the output of a brace expansion (or filename expansion),
    you can run the command prefixed with **`echo`**: this prints the command
    that would be executed to the terminal without running the command.

      ```sh
      echo mkdir -p species_by_{genus/{Dendrolagus,Crocidura},common_name/{B,R}}
      ```

   <br>
   </details>

2. **Copy files** using the **`cp`** command:
   * From the directory `exercise_2/RedList_mammals`, make a copy of all files
     of the genuses `Dendrolagus` and `Crocidura` into their respective
     sub-directories in `species_by_genus`.
   * From the directory `exercise_2/RedList_mammals`, copy the file for the
     [Red Wolf](https://en.wikipedia.org/wiki/Red_wolf) (*Canis rufus*) to the
     directory `species_by_common_name`.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     # Copy files for the "Dendrolagus" genus.
     cp ../exercise_2/RedList_mammals/Dendrolagus_* species_by_genus/Dendrolagus/
     
     # Copy files for the "Crocidura" genus.
     cp ../exercise_2/RedList_mammals/Crocidura_* species_by_genus/Crocidura/

     # Copy the file for the Red Wolf.
     cp ../exercise_2/RedList_mammals/Canis_rufus species_by_common_name/
     ```

   <br>
   </details>

3. **Move and rename** the Red Wolf file with the **`mv`** command:
   * Enter the `species_by_common_name` directory.
   * In the directory, move the file `Canis_rufus` into subdirectory `R`.
   * Rename the `Canis_rufus` file you just moved into the subdirectory `R` to
     the common name of the species: `Red_wolf`.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    cd species_by_common_name/
    mv Canis_rufus R/            # Move the file into its subdirectory.
    mv R/Canis_rufus R/Red_wolf  # Rename the file to the common name of the species.
    ```

   <br>
   </details>

4. **Copy and rename files in a single the `cp`** command:
   Similarly to what we did for the Red Wolf file, we will now copy and
   rename the file for the [Black Rhinoceros](https://en.wikipedia.org/wiki/Black_rhinoceros)
   *Diceros bicornis*, but this time we will copy and rename the file
   *in a single step* using the **`cp`** command.
   * Copy the file `Diceros_bicornis` from its original location (in
     `exercise_2/RedList_mammals`) into `species_by_common_name/B`, while
     directly renaming it to the common name of the species: `Black_rhino`.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
     # Note: this assumes the current working directory is "species_by_common_name".
     cp ../../exercise_2/RedList_mammals/Diceros_bicornis B/Black_rhino
     ```

   <br>
   </details>

5. **Copy, rename and delete directories**:
   * Change directory to the root of the `exercise_3/` directory.
   * Copy the entire directory `species_by_genus/Dendrolagus` - with all its
     content - to the root of `exercise_3`.  
     :target:
     **Hint:** to make a **recursive** copy of a directory, the option is
     `-r`/`--recursive`.
   * Rename the directory to `Tree-kangaroos`.
   * Delete the directory `Tree-kangaroos` and its content **in a safe way**.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    cd ..                                  # Change directory to `exercise_3`.
    cp -r species_by_genus/Dendrolagus/ .  # Copy the directory and its content.
    mv Dendrolagus/ Tree-kangaroos         # Rename the directory.
    ```

    To delete the directory in a safe way, we first delete all files inside it,
    and then delete the empty directory with **`rmdir`**, which
    **only deletes a directory if it is empty**. This is a safety behavior to
    avoid deleting large number of files by mistake.

    ```sh
    rm Tree-kangaroos/*
    rmdir Tree-kangaroos
    ```

    :kangaroo:
    **Note:** the faster way to delete the directory and all of its content is
    to use the command: `rm -rf Tree-kangaroos`.
    * :warning:
      This recursively deletes the directory, and therefore one has to be
      **very careful** to delete the correct directory, as you can otherwise
      very quickly delete large amounts of data by mistake, which can be
      problematic as **there is no command to undo file deletion**.

   <br>
   </details>

<br>

### Additional Tasks 3

6. **At the root of `exercise_3/`, create a new directory** named
   `species_by_binomial_name` and enter it.

7. **Inside this directory, create sub-directories named `A`, `B`, `C`, ... `Z`**
   (i.e. one directory for each letter of the alphabet).

   To avoid doing this tedious work manually, you can use a **for loop** very
   similar to this example:

    ```sh
    for x in {A..Z}; do echo ${x}; done
    ```

   Try to run the above code in your shell (it will only print things to the
   screen without creating anything on disk). Then adapt the `for` loop so that
   it creates the directories from `A` to `Z`.

   :sparkles:
   **Note:** in this specific case, a **for loop** is not even necessary, as we
   can also simply use
   **[brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion)**:
   `mkdir {A..Z}`.

8. **Copy all files from `exercise_2/RedList_mammals` into their correct subdirectory**,
   i.e. the subdirectory that corresponds to the first letter of the file's
   Genus name.  
   For example: `Marmota_vancouverensis` should go into sub-directory `M`
   because the first letter of the genus name is `M`.

   You can again do this using a `for` loop. Here is an example you can run as
   a test, and then adapt to copy the files into the correct sub-directory.

   ```sh
   for x in {A..Z}; do ls ../../exercise_2/RedList_mammals/${x}* ; done
   ```

   Note that when running the `for` loop, you will get some
   **warning messages**, because the genuses present in `RedList_mammals` do
   not cover all letters of the alphabet. However, this is not a problem here
   because it does not prevent the `for` loop from running to the end.

<br>

<details><summary><b>:white_check_mark: Additional tasks solution</b></summary>
<p>

```sh
# 6. Create and enter the new directory.
mkdir species_by_binomial_name
cd species_by_binomial_name/

# 7. Create directories "A" to "Z" with a for loop.
for x in {A..Z}; do mkdir ${x}; done
# Alternative: use brace expansion.
mkdir {A..Z}

# 8. Copy species file names into the correct directory.
#    Note that letters that do not have any matching genus will print a warning
#    to the terminal.
for x in {A..Z}; do cp ../../exercise_2/RedList_mammals/${x}* ${x}/; done
ls -l ./*
```

</p>
</details>

<br>
<br>
<br>

## Exercise 4 - Finding files [~15 min]

:triangular_flag_on_post:
**Objective:** learn to use the **`find`** command.

<br>

Enter the `exercise_4` directory and perform the following tasks using the
**`find`** command:

1. **Find all files with a `.png` extension** located anywhere in `exercise_4/`.
   * Make sure to list *only* files, and not directories.  
   * :dart:
     **Hints:**
     * Use **`-type f`** to restrict the search to files (excludes directories).
     * You should find a total of 6 `.png` files.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     cd exercise_4/
     find . -type f -name "*.png"
     # -> There are 6 ".png" files, all located in ./images/img.png/
     ```
  
   :warning:
   It is good practice to **always pass the search patten between quotes** in
   order to avoid accidental **filename expansion**. To convince yourself, you
   can try the following.

     ```sh
      # Create a test file with a .png extension.
      touch test.png

      # Now compare the output of the 2 commands:
      find . -type f -name *.png
      find . -type f -name "*.png"
     ```

   <br>
   </details>

2. **Find files with either a `.jpeg` or `.png` extension**.
   * As before, directories should be excluded from the search results.  
   * :dart:
     **Hint:**
     * Use the **`-or`** operator to combine multiple search conditions.
     * You should find a total of 15 files.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    :warning: Note that **`-type f`** must be repeated for each condition.

     ```sh
     find . -type f -name "*.png" -or -type f -name "*.jpeg"
     # -> There are 9 ".jpeg" files, located in ./images/img.jpeg/
     # -> There are 6 ".png" files, located in ./images/img.png/
     ```
  
    :sparkles:
    If you are familiar with
    [regular expressions](https://www.regular-expressions.info), you can also
    use them with the `find` command by passing the **`-regex`** option.
    Here we find all `.jpeg` or `.png` files (same as above) using a regexp:

     ```sh
     find . -type f -regex ".*\.jpeg\|.*\.png"
     ```

   <br>
   </details>

3. Find all `.jpeg` files **larger than `15 kB`**.

   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    find . -type f -name "*.jpeg" -size +15k
    ```

   <br>
   </details>

<br>

### Additional Tasks 4

Try to use the **`-exec` option of `find`** to display full details (as given
by the `ls -lh` command) of the files that are found in point 3 of the main
exercise above.

One possible way to use the **`-exec`** options is as follows:

* **`-exec <command> "{}" +`**, where:
  * `<command>` is the custom command to execute.
  * `"{}"` is the placeholder that will be expanded to the files found by `find`.

Your output for all `.jpeg` files larger than `15 kB` should look like this:

```sh
-rw-rw-r-- 1 bob bob 25K Jan  8 11:16 ./images/img.jpeg/linux_logo.jpeg
-rw-rw-r-- 1 bob bob 26K Jan  8 11:40 ./images/img.jpeg/linux_gentoo_logo.jpeg
-rw-rw-r-- 1 bob bob 16K Jan  8 11:36 ./images/img.jpeg/linux_suse_logo.jpeg
```

<details><summary><b>:white_check_mark: Solution</b></summary>

```sh
find . -type f -name *.jpeg -size +15k -exec ls -lh "{}" +
```

:sparkles:
**Note:** the following syntax is also possible:

```sh
find . -type f -name *.jpeg -size +15k -exec ls -lh "{}" \;
```

The difference between **`-exec ls -lh "{}" +`** and **`-exec ls -lh "{}" \;`**
is that:

* With **`+`**, all matching files are passed to the `-exec` command.
  In our `ls` example, this is equivalent to running:

  ```sh
  ls ./images/img.jpeg/linux_logo.jpeg ./images/img.jpeg/linux_gentoo_logo.jpeg ./images/img.jpeg/linux_suse_logo.jpeg
  ```

* With **`\;`**, an individual command is run for each file that is found.
  In our `ls` example, this is equivalent to running:

  ```sh
  ls ./images/img.jpeg/linux_logo.jpeg
  ls ./images/img.jpeg/linux_gentoo_logo.jpeg
  ls ./images/img.jpeg/linux_suse_logo.jpeg
  ```

In the case of the `ls` command, this does not change much (maybe there is a
slight performance advantage of running a single `ls`), but there are commands
that accept only a single file as argument, in which case the solution with
`"{}" +` would not work because all files are passed to the command in a single
call.

<br>
</details>

<br>
<br>
<br>

## Exercise 5 - Display file content [~10 min]

:triangular_flag_on_post:
**Objective:** get familiar with shell commands that display text file content:
**`head`**, **`tail`**, **`cat`** and **`less`**. Also includes a basic usage
of **`tar`**.

<br>

Enter the `exercise_5/` directory and list its content. You should see that it
contains a single file named `data.tar.gz`. This is a compressed (`.gz`) TAR
archive (`.tar`).

Your first task in this exercise is to:

* List the content of the `data.tar.gz` archive file. You should see that it
  contains a single file named `protein_sequences.fasta`.
* Extract the `protein_sequences.fasta` file from the archive (i.e. decompress
  and untar the archive file).

  <br>
  <details><summary><b>:white_check_mark: Solution</b></summary>

     ```sh
     # List the content of the TAR archive file.
     tar -ztvf data.tar.gz

     # Extract data from the archive file.
     tar -zxvf data.tar.gz
     ```

   <br>
   </details>

<br>

Now that we extracted the data from the archive file, perform the following
tasks on the `protein_sequences.fasta` file:

1. **Display the start/end of the file** using the **`head`** and **`tail`**
   commands:
   * Display the first 10 lines of the file.
   * Display the last 5 lines of the file.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    cd exercise_5/protein_sequences.fasta 
    head protein_sequences.fasta           # No need to specify "-n 10", as 10 is the default value.
    tail -5 protein_sequences.fasta
    ```

   :fire:
   **Tips:**
   * To display the entire file **except for the last `X` lines** we can use
     **`head -n-X`** (replace `X` by the number of lines you want to skip
     at the end of the file).
   * Conversely, **`tail -n+X`** will skip the first `X` lines, then print all
     remaining lines until the end of the file.

   <br>
   </details>

2. **Count the number of lines** in the file using the **`wc`** command:
   * Count only the number of lines in the file.
   * Count only the number of words in the file.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    wc -l protein_sequences.fasta   # 19222 lines.
    wc -w protein_sequences.fasta   # 51914 words.
    ```

   <br>
   </details>

3. **Display the content** of the file using the **`cat`** command.
   * :question:
     **Question:** why is `cat` not the most adapted program here ? What could
     we use instead ?

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    cat protein_sequences.fasta
    ```

   * `cat` is not ideal here because the file is large. While `cat` is often
     hand to display small files, the primary purpose of `cat` is actually to
     con**cat**enate 2 or more files together (this is where the command
     got its name from). An example of how to concatenate files with `cat` is
     given in the **Additional Tasks** section below.
   * To display the content of large files, `less` is generally more
     appropriate.

   <br>
   </details>

4. **Display, navigate and search** the file with **`less`**:
   * Open the file using `less`.
   * Add lines numbers to the display using the **`-N` option**.
   * Navigate the file using the space bar and arrows.
   * Search for the pattern `isoform` using the command `/<search term>`, then
     navigate through the matches with the keys `n` and `N`.
   * Close the file (exit `less`) with pressing the **`q`** key.

   <br>
   <details><summary><b>:white_check_mark: Solution</b></summary>

    ```sh
    less protein_sequences.fasta
    less -N protein_sequences.fasta   # Line numbers can also be added/removed
                                      # after a file was opened with "-N" + "enter".
    ```

   <br>
   </details>

<br>

### Additional Tasks 5

5. **Usage of `cat` to concatenate files**.  
   The primary purpose of `cat` is not to display files (as we have seen above),
   but to con**cat**enate 2 or more files together (this is where the command
   got its name from).
   `cat` concatenates files by pasting their content one after the other, in
   the order in which the files are passed to the command.

   Let's try the following example:

   * We start by **creating 2 files to concatenate** (`file_1` and `file_2`):

     ```sh
     head -n5 protein_sequences.fasta > file_1
     tail -n5 protein_sequences.fasta > file_2
     ```

   * We can now **concatenate these 2 files** into a new file (`file_3`):

     ```sh
     cat file_1 file_2 > file_3
     
     # Same as above, but using filename expansion (globbing).
     cat file_? > file_3
     ```
  
   * If you display the content of `file_3` with `cat`, you will see that it
     contains 10 lines: the content of both `file_1` and `file_2`.

   * :sparkles:
     **Bonus:** we could also create `file_3` of the example above without
     creating any intermediate file. This is done using a method called
     **[process substitution](https://www.gnu.org/software/bash/manual/bash.html#Process-Substitution)**
     and allows to treat the output of a command as an input file. The syntax
     of process substitution is **`<(  )`**.

      ```sh
      cat <( head -n5 protein_sequences.fasta ) <( tail -n5 protein_sequences.fasta )
      ```

   * :sparkles:
     **Note:** to concatenate multiple files by columns, use the **`paste`**
     command.

6. **Display *only* the line 100 of `protein_sequences.fasta`** by using a
   combination of **`head`** and **`tail`**.

   For this you will need to use the the **`|` (pipe) operator**, that allows
   to redirect the output of one command into another command.

   <details><summary><b>:white_check_mark: Solution</b></summary>

   **`head`** and **`tail`** can be combined to display any section of a file.
   Here is how we print the line 100 of the file:

    ```sh
    head -n100 protein_sequences.fasta | tail -n1  # Print the 100th line.
    ```

   <br>
   </details>

<br>
<br>
<br>

## Exercise 6 - Convert, sort, compare and merge tabulated data [~30 min]

:triangular_flag_on_post:
**Objective:** get familiar with some of the basic Linux/UNIX core utilities -
**`cut`**, **`sort`**, **`tr`**, **`paste`**, **`diff`**.

### Exercise context

In this exercise, we will be working with **3 tabulated data files**
containing replicates from a
[micro-array experiment](https://en.wikipedia.org/wiki/DNA_microarray).  

* The files are located in `exercise_6/micro-array/data/`.
  * `exercise_6/micro-array/data/array_data-1.csv`
  * `exercise_6/micro-array/data/array_data-2.csv`
  * `exercise_6/micro-array/data/array_data-3.csv`
* Each file contains 2 columns, separated by `;` characters:
  * **Column 1:** gene name (`ProbeID`).
  * **Column 2:** level of gene expression in each replicate
    (`Sample1`, `Sample2`, `Sample3`).

```sh
# A view of the first 4 lines of each file.
==> array_data-1.csv <==
ProbeID;Sample1
1007_s_at;10.93
1053_at;8.28
117_at;3.31

==> array_data-2.csv <==
ProbeID;Sample2
1552390_a_at;2.76
1552389_at;3.4
1552388_at;2.61

==> array_data-3.csv <==
ProbeID;Sample3
1007_s_at;11.19
1053_at;8.06
117_at;3.13
```

**Our objective is to merge these three files** into a single tab-delimited
file with 4 columns: `ProbeID` (gene name), `Sample1`, `Sample2` and `Sample3`
(the gene expression levels recorded in each replicate of the experiment).

Additionally, the output file format should be **tab-delimited values** rather
than semi-column separated values as is the case in the input files.

Our final output should thus look like this:

```sh
ProbeID     Sample1   Sample2   Sample3
117_at      3.31      3.41      3.13
121_at      4.42      4.32      4.46
1007_s_at   10.93     11.44     11.19
1053_at     8.28      7.54      8.06
...
```

Please note that one complication comes from the fact that the order of the
genes in the input files is **not the same** across all files... Therefore the
values from the input files **will have to be sorted** before the files can
be merged by columns.

As this exercise is a bit more complicated, we will decompose it into several
steps.

<br>

### Data exploration

Enter the directory `exercise_6/micro-array/data` and have a look at the
3 input files using `less` or `head`, to get familiar with their structure
and content.

<details><summary><b>:white_check_mark: Solution</b></summary>

```sh
cd exercise_6/micro-array/data/
head array_data-*

# Open a file with `less`.
less array_data-1.csv       # Reminder: to exit `less`, press "q".
```

<br>
</details>

### Step 1: conversion to tab-delimited values

The original files contain tabulated data separated by a **`;`** (semi-column)
character. We would like to change this separator to a Tab **`\t`**.

* Convert the delimiters from `;` to `\t` (tab) using the command **`tr`**.
* Save the converted content into a new file with a `.tsv` extension. E.g. the
  converted version of `array_data-1.csv` should be named `array_data-1.tsv`.
* :dart:
  **Hints**:
  * To convert (translate) one character to another in a file, the `tr`
    command looks like: `tr "CHARACTER TO REPLACE" "NEW CHARACTER"`.
  * `tr` is a command that only takes input from the standard input (*stdin*),
    i.e. it does not accept a file name as argument. Therefore, you need to
    redirect the content of a file to standard input with `< FILE_NAME`.

<details><summary><b>:white_check_mark: Step 1 solution</b></summary>

```sh
tr ";" "\t" < array_data-1.csv > array_data-1.tsv
tr ";" "\t" < array_data-2.csv > array_data-2.tsv
tr ";" "\t" < array_data-3.csv > array_data-3.tsv
head *.tsv

# Loop shortcut:
for i in $(seq 1 3); do tr ';' '\t' < array_data-${i}.csv > array_data-${i}.tsv; done
```

:penguin:
**Fun fact:** `tr` is one of the (few) commands that
**does not accept a file as input**, it only accepts input from *stdin*.
This is why we must use `tr < file` or `cat file | tr` to pass input to `tr`.

<br>
</details>

### Step 2: sort the files

Before we can merge the content of the 3 `array_data-*.tsv` files, we have to
make sure that the order of rows in each file (i.e. the order of genes) are the
same in each file.

If you look at the files, you will see that this is not the case. Therefore the
files need to be sorted by their 1st column (`ProbeID`).

* Sort each `array_data-*.tsv` file by its `ProbeID` column using the
  **`sort`** command.
* Make sure that the **header line** of the file remains at the top after the
  sorting operation.  
  * :dart:
    **Hint:** the header line is the only line that starts with a letter. We
    can therefore take advantage of *numerical sorting* that sorts letters
    before numbers. You can have a look at `man sort` (the help for the `sort`
    command) to find the right option.
* Save the sorted output to files named `array_data-sorted-*.tsv`.

<details><summary><b>:white_check_mark: Step 2 solution</b></summary>

```sh
sort -n array_data-1.tsv > array_data-sorted-1.tsv
sort -n array_data-2.tsv > array_data-sorted-2.tsv
sort -n array_data-3.tsv > array_data-sorted-3.tsv
head *sorted-?.tsv

# Loop shortcut:
for i in $(seq 1 3); do sort -n array_data-${i}.tsv > array_data-sorted-${i}.tsv; done
```

<br>
</details>

### Step 3: verify the file sorting

In this step, we will double-check that the sorted files we created at the
previous step (`array_data-sorted-*.tsv`) have the same number of lines
and that the genes on those lines are in the same order.

To verify this, the idea is to **extract the first column** (the gene names)
from the sorted files into temporary files, and verify that all those files
(that only contain the gene names) are identical.

Proceed as follows:

* **Use the `cut` command** to extract the first column (`ProbeID`) of each
  `array_data-sorted-*.tsv` file. Save the output to temporary files named
  `tmp-1.tsv`, `tmp-2.tsv`, and `tmp-3.tsv` (these files should contain a
  single column).
* **Compare the content of the 3 `tmp-*.tsv` files** using the commands
  `diff -s tmp-1.tsv tmp-2.tsv` and `diff -s tmp-1.tsv tmp-3.tsv`.
* If all `tmp-*.tsv` files are the same (and they should), you can then delete
  these files. Their only purpose was to allow us to check that all files
  have their lines sorted in the same order.

<details><summary><b>:white_check_mark: Step 3 solution</b></summary>

```sh
# Extract the first column of each file into a temporary file.
cut -f1 array_data-sorted-1.tsv > tmp-1.tsv
cut -f1 array_data-sorted-2.tsv > tmp-2.tsv
cut -f1 array_data-sorted-3.tsv > tmp-3.tsv

# Loop shortcut:
for i in $(seq 1 3); do cut -f1 array_data-sorted-${i}.tsv > tmp-${i}.tsv; done

# Compare files that contain only the first column:
diff -s tmp-1.tsv tmp-2.tsv
diff -s tmp-1.tsv tmp-3.tsv
rm tmp-?.tsv
```

:sparkles:
**Bonus:** if we want to avoid creating temporary files, we can use a
functionality of the shell called
**[process substitution](https://www.gnu.org/software/bash/manual/bash.html#Process-Substitution)**,
where the output of a command is treated as an input file.

```sh
diff -s <(cut -f1 array_data-sorted-1.tsv) <(cut -f1 array_data-sorted-2.tsv)
diff -s <(cut -f1 array_data-sorted-1.tsv) <(cut -f1 array_data-sorted-3.tsv)
```

<br>
</details>

### Step 4: Merge the sorted files

In this final step, we concatenate the content of the `array_data-sorted-*.tsv`
files to produce a final file (`final.tsv`) with 4 columns:
`ProbeID`, `Sample1`, `Sample2`, and `Sample3`.

* Use **`paste`** to concatenate the content of the `-sorted-*.tsv` files.
* Use **`cut`** to remove the duplicated `ProbeID` columns.
* These two steps can be performed in a single command line by using a pipe
  operator (`|`) to pass the output of `paste` to `cut`.

Your final output file should look like this:

```sh
ProbeID     Sample1   Sample2   Sample3
117_at      3.31      3.41      3.13
121_at      4.42      4.32      4.46
1007_s_at   10.93     11.44     11.19
1053_at     8.28      7.54      8.06
1255_g_at   1.8       1.7       1.75
...
```

<details><summary><b>:white_check_mark: Step 4 solution</b></summary>

```sh
paste array_data-sorted-*.tsv | cut -f 1,2,4,6 > final.tsv
head final.tsv
```

:sparkles:
**Note:** to learn how to do the entire processing we did in this exercise
**in a single command**, look at the Additional Tasks 6 section below. It
also shows how the processing can be done using the `join` command, but it's
actually more complicated in this case.

<br>
</details>

<br>

### Additional Tasks 6

We will now try to re-write the entire process sorting converting, sorting and
merging our 3 original data files (steps 2, 3 and 5 above) as a single command

For this you will need to use the following shell functionalities:

* The **Pipe operator `|`**, to redirect the input of one command into the
  next.
* The **[process substitution](https://www.gnu.org/software/bash/manual/bash.html#Process-Substitution)**
  syntax `<( command )`, to treat the output of a command (or of a series of
  commands) as a virtual file from which data can be read.

:dart:
**Hint:** this task is a bit more complicated, so to get you started, here is
an example to give you some inspiration. You can run the command bellow in
your shell:

```sh
# Sort and merge the 2nd column (gene expression) of 2 of our input files:
paste <(sort -n array_data-1.csv | cut -f2 --delim=";") <(sort -n array_data-2.csv | cut -f2 --delim=";") | head
```

<details><summary><b>:dart: Additional Hint</b></summary>

Here is scaffold of the solution with the **`<()`** and **`|`** placed at the
correct locations. What is left to do is to replace the textual descriptions
with the correct commands.

```sh
paste <( "sorted content of array_data-1.csv" | convert ; to \t" ) \
      <( "sorted array_data-2.csv | keep only 2nd column" ) \
      <( "sorted array_data-3.csv | keep only 2nd column" ) > final_2.tsv
```

</details>

<details><summary><b>:white_check_mark: Solution</b></summary>

Here is how we could do the whole processing of this exercise in a single
command without creating any intermediate files.

```sh
paste <(sort -n array_data-1.csv | tr ";" "\t") \
      <(sort -n array_data-2.csv | cut -f2 --delim=";") \
      <(sort -n array_data-3.csv | cut -f2 --delim=";") > final_2.tsv

# Compare the new output file with the one we produced earlier:
diff -s final.tsv final_2.tsv
diff -s final*.tsv       # Same as above, using filename expansion.
diff -s final{,_2}.tsv   # Same as above, using brace expansion.
```

:pushpin:
An alternative is to use the **`join`** command. Unfortunately, the `join`
command only allows to join 2 files at a time, so in this case the solution
ends-up being more complicated (`join` would however be much better in cases
where we want to join files that have missing rows - i.e. not all files have
all the rows):

```sh
join --check-order -o 0 1.2 1.3 2.2 -1 1 -2 1 -t ";" \
     <( join --check-order -o 0 1.2 2.2 -1 1 -2 1 -t ";" \
             <( sort array_data-1.csv ) \
             <( sort array_data-2.csv ) \
      ) \
     <( sort array_data-3.csv ) | sort -n | tr ";" "\t" > final_3.tsv

# Compare the new output file with the one we produced earlier:
diff -s final{,_3}.tsv
```

</details>

<br>
<br>
<br>

## Exercise 7 - Introduction to `grep` [~30 min]

:triangular_flag_on_post:
**Objective:** learn the basic usage of **`grep`** and practice piping the
output of one command to the input of the next command.

In this exercise, we will work with a copy of the file
`exercise_5/protein_sequences.fasta`. This file is a so-called
[FASTA file](https://en.wikipedia.org/wiki/FASTA_format). FASTA is a
text-based format to represent nucleotides or protein sequences.

* **FASTA files** can contain one or more sequences.
* Each new sequence starts with a **sequence header** line, which starts with
  the character **`>`**. A sequence header is always on a single line.
* Each sequence header is followed by one or more lines that contain the
  nucleotide or amino acid sequence of the sequence.

Here is an example of a section of a FASTA file:

```sh
>sp|P18823|ACCD_PEA Carboxyl transferase OS=Pisum sativum GN=accD PE=1 SV=3
MINEDPSSLTDMDNNIDSWKNNSENSSYSHADSLADVSNIDNLLSDKIFSIRDSNSNIYD
IYYAYDTNDTNITKYKWTNNINRCIESYLRSQICEDIDFNSDICDKVQRTIIILIRSTND
NDISDTNDISDTNDTNDTNAIYDPFDISDTNDTN
>sp|P09339|ACON_BACSU Aconitate hydratase OS=Bacillus subtilis GN=citB PE=1 SV=4
MANEQKTAAKDVFQARKTFTTNGKTYHYYSLKALEDSGIGKVSKLPYSIKVLLESVLRQV
DGFVIKKEHVENLAKWGTAELKDIDVPFKPSRVILQDFTGVPAVVDL

```

<br>

### Part A - basic `grep` usage

Enter the directory `exercise_7` and
**make a copy of the file `exercise_5/protein_sequences.fasta`**
in your current working directory. Name the copy of the file `sequences.fasta`.

:sparkles:
**Note for Linux/Mac users:** if you are using Linux/Mac, you may also create
a **symlink** instead of copying the file. The command is the following:

* `ln -s ../exercise_5/protein_sequences.fasta sequences.fasta`
* A symlink creates a pointer to a file, without making an actual copy of it.
* Symlinks are not supported on Windows (except if using WSL and working on a
  non-windows partition).

Have a look at the `sequences.fasta` file - e.g. using the `less` command -
then **answer the following questions using the `grep` command**:

* How many sequences are there in the file?  
  :dart: **Hint:** count the number of header lines in the file.
* How many entries are from `Staphylococcus`?
* Display header lines that are *not* from `Staphylococcus`?  
  :dart: **Hint:** you will need to pipe together 2 `grep` commands using the
  **`|` (pipe)  operator**.

Here is a reminder of some of the `grep` options:

* **`-i`**: case insensitive search.
* **`-c`**: suppress normal output; instead print the count of matching lines.
* **`-o`**: print only matching content, not the entire line.
* **`-n`**: add the line number in front of printed output.
* **`-v`**: inverted search - print lines that do *not* match the pattern.

<br>

<details><summary><b>:white_check_mark: Solution Part A</b></summary>

```sh
cd exercise_7/
cp ../exercise_5/protein_sequences.fasta sequences.fasta

# Count the number of sequences in the file:
grep -c "^>" sequences.fasta   # -> 3325 sequences.

# Count the number of sequences from Staphylococcus
# Note the use of the `-i` option of `grep` ("case insensitive search").
grep -ci "os=staphylococcus " sequences.fasta   # 141 sequences.

# Display the header lines of sequences that are not from Staphylococcus.
grep "^>" sequences.fasta | grep -vi "os=staphylococcus "
grep "^>" sequences.fasta | grep -vi "os=staphylococcus " | wc -l   # The sequence count is 3184.
```

</details>

<br>

### Part B - extract the top 10 most-frequent genus

In the second part of this exercise, your task is to
**display the 10 most frequent genuses** found in the sequences of the
`sequences.fasta` file, along with their frequency/count (i.e. the number of
sequences for each of the 10 most-frequent genus in the file).

Here is a suggested way to perform this task:

1. Isolate the header lines.
2. Isolate the genus name from each line. To do this, you can take advantage
   of the *controlled vocabulary* in the file: the organisms name is always
   prefixed with `OS=`.
3. Sort the genus names, compute their frequency and keep only a single
   instance of each genus name.
4. Sort the genus by frequency and keep only the 10 most frequent.

:dart:
**Hints:**

* The steps above are best done as part of a pipeline: use the
  **`|` (pipe)  operator** to pipe the output of one command into the next.
* When building the pipeline and doing tests, you can temporarily end your
  pipeline with **`| head`** so that you avoid printing the whole file each
  time.

<details><summary><b>:dart: Additional Hints</b></summary>

Here are some commands and their options that are useful for this exercise:

* **`uniq -c`**: the `-c/--count` option prefixes each line with the number of
                 occurrences.
* **`sort -nr`**:
  * `-n/--numeric-sort` sorts numerically instead of alphabetically.
  * `-r/--reverse` sorts in decreasing order.
* **`grep -o`**: the `-o/--only-matching` option returns only the matching part
  of a line instead of the entire line (the default grep behavior).

</details>

<br>

<details><summary><b>:white_check_mark: Solution Part B</b></summary>
<p>

There are multiple ways to perform this task, here are a few possibilities.

* :sparkles:
  **Note:** some pipelines below make use of the `grep` option **`-o`**, which
  instructs `grep` to only output the actual matching pattern instead of the
  entire line on which the match is found.

```sh
grep "^>" sequences.fasta | cut -f2 --delim="=" | cut -f1 --delim=" " | sort | uniq -c | sort -nr | head

grep -o "OS=[a-zA-Z]*" sequences.fasta | cut -f2 --delim="=" | sort | uniq -c | sort -nr | head

# Same as above, but using the "[[:alpha::]]" syntax to indicate we only want
# to match alphabetic letters and not e.g. spaces (or numbers).
grep -o "OS=[[:alpha:]]*" sequences.fasta | cut -f2 --delim="=" | sort | uniq -c | sort -nr | head

# Output of the pipe: the 10 most frequent genus and their frequency in the file.
    168 Arabidopsis
    166 Escherichia
    163 Bacillus
    152 Homo
    141 Staphylococcus
    134 Mus
    111 Oryza
     84 Salmonella
     83 Rattus
     72 Mycobacterium
```

Here is another solution that makes use of a more complicated
**regular expression** to directly isolate the genus name. For this we must:

* Use `grep` with "Perl"-style regular expressions by adding the **`-P`**
  option.
* Use a **lookbehind match**: `(?<=OS=)` matches something located behind the
  pattern `OS=`.

```sh
grep -oP "(?<=OS=)[a-zA-Z]+ " sequences.fasta | sort | uniq -c | sort -nr | head
```

:see_no_evil:
**[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression)** are
a powerful tool to do sophisticated pattern matching. However they are beyond
the scope of this course.

</details>

<br>

### Additional Tasks 7

This is not an easy one, but it's the last!

Our objective is to write a short **`for` loop** that performs the task
of copying each species files found in the `exercise_2/RedList_mammals`
directory into the correct directory for its genus in a `species_by_genus`
directory.

So basically, instead of only doing it for 2 genus manually as we did in
exercise 3, we want to have it done automatically for all genuses.

:dart:
**Hints:** this task is more difficult and uses a few concepts that were not
presented in the course, such as:

* **`for` loops** to repeat a number of instructions multiple times while
  iterating over a range of values. In our case, we want to iterate over the
  list of genuses.
* **Variables**: in bash, variables can be:
  * Created using `variable_name=value`.
  * Accessed using `${variable_name}`.

Here is a scaffold of one possible solution to get you started.

```sh
# Enter the "exercise_7" directory and create a new "species_by_genus"
# directory.
cd exercise_7/
mkdir species_by_genus

# Save the "RedList_mammals" directory location in a variable, so it will be
# easy to access later.
red_list_dir=../exercise_2/RedList_mammals

# Loop through all genus values and copy the files for each in the correct
# sub-directory of "species_by_genus".
for genus in $( <pipeline that returns the list of genus> ); do
    mkdir species_by_genus/${genus}      # Create directory for genus.
    cp ${red_list_dir}/... ...           # Copy files for genus.
done

# List all the copied files to see if the result is correct.
ls species_by_genus/*
```

What you have left to do in the code above is to:

* Replace `<pipeline that returns the list of genus>` with a series of commands
  that will produce the list of unique genus present in `RedList_mammals`.
* Replace `cp ...` with the proper command to copy all files for a given
  genus.

<br>

<details><summary><b>:white_check_mark: Solution</b></summary>

```sh
# Enter the "exercise_7" directory and create a new "species_by_genus"
# directory.
cd exercise_7/
mkdir species_by_genus

# Save the "RedList_mammals" directory location in a variable, so it will be
# easy to access later.
red_list_dir=../exercise_2/RedList_mammals

# Loop through all genus values and copy the files for each in the correct
# sub-directory of "species_by_genus".
for genus in $( ls ${red_list_dir} | cut -f1 --delim="_" | sort | uniq ); do
    mkdir species_by_genus/${genus}                          # Create dir for genus.
    cp ${red_list_dir}/${genus}_* species_by_genus/${genus}  # Copy files for genus.
done

# List all the copied files to see if the result is correct.
ls species_by_genus/*
```

</details>

<br>
