# Exercises - First steps with UNIX

<br>

## Before you start

Please read the following instructions before starting the exercises:

* **Exercise material setup:** download the
  [exercises.zip](exercises.zip) archive file to your local computer and
  unzip it. This will unpack a directory named `exercises`, with all the data
  needed for the course exercises.

* **Exercise solutions:** all exercises and Additional Tasks section have their
  solution embedded in this document. The solutions are hidden by default, but
  you can reveal them by clicking on the drop-down menu, like this one:
  
  <details><summary><b>Exercise solution (click me)</b></summary>
  :sparkles: This reveals the answer :sparkles:
  </details>

  We encourage you to *not* look at the solutions too quickly, and try to
  solve the exercises without it. Remember that you can always ask the course
  teachers for help.

* **Additional Tasks:** at the end of each exercise, you will find a section
  named **Additional Tasks**. These sections contain tasks to complete
  **if you have the time and after having completed the main exercise**. The
  Additional Tasks sections will not be corrected in class, but their solution
  is given in this document.

<br>
<br>
<br>

## Exercise 1 - Navigating the filesystem in command line [~20 min]

**Objective:** get familiar with navigating the directory tree and listing
the content of directories.

1. **Print your current working directory** with the `pwd` command. This will
   show you where you currently are in the directory tree.

2. **Navigate to the `exercises/` directory** (the one you unpacked from the
   zip archive file), and then enter the `exercise_1` subdirectory.

3. **Try to run the commands `cd .` and `cd ..`**  
   What happens? What does `.` and `..` stand for?

4. **List the content** of the `exercise_2/` directory with `ls`, `ls -l`,
   `ls -lh`, and `ls -lha`.
   * **Question:** what do the `-l`, `-h` and `-a` options do?
   * :dart:
     **Hint:** you can use `man ls` to display the help for the `ls` command.
     To exit the help, simply type `q` on your keyboard.
   * :sparkles:
     *Notes:*
     * One-letter options can be grouped together, so `ls -lha` is the
       same as `ls -l -h -a`.
     * Some options have both a "short" and a "long" form. E.g. `ls -ah`
       is the short form for `ls --all --human-readable`.

5. **List the content of the directory in chronological order** (oldest file
   first) and in reverse chronological order (newest file first).

:fire:
**Tip:** a very handy functionality that the shell provides is the ability to
**auto-complete file/directory names**. You simply have to start typing the
start of a file/directory name, and then press on **TAB** on your keyboard. The
shell will autocomplete (as much as possible) the file name. You can try this
functionality to autocomplete the name of the file
`a_regular_file_with_a_really_long_name.md`.

<br>
<details><summary><b>Exercise solution</b></summary>
<p>

1. Printing the current working directory:

    ```sh
    pwd
    ```

2. Navigate to `exercises/exercise_1`:

    ```sh
    cd /path/to/directory/exercises
    ls -l
    cd exercise_1
    pwd
    ls -l
    ```

   :sparkles: changing directory to `exercise_1` can of course also be done
   in a single command:

    ```sh
    cd /path/to/directory/exercises/exercise_1
    ```

3. The **`.`** symbol is a **shortcut for the current directory**. So running
   `cd .` has no effect since it simply changes to the same directory we are
   already in.
   The `.` shortcut is useful in some situations. E.g. if you want to copy
   a file to the current directory you can do `cp /file/to/copy .`, or you
   can run an executable located in the current directory with `./run_me.sh`.

   The **`..`** symbol is a **shortcut to the parent directory**. These
   shortcuts can be combined, so e.g. `cd ../..` will go up to levels in the
   directory tree.

4. Listing the content of the `exercise_1/` directory with different `ls`
   options. The effect of the different options is described in the comments
   of the code block.

    ```sh
    ls       # Prints the names of files and directories
    ls -l    # List content of the subdirectory in "long listing" format. This
             # provides additional details for each file/directory, such as
             # its permissions, its size and its last modified date.
    ls -lh   # Adding the "-h" option displays file sizes in "human readable"
             # format. The size of files are shown in kB, MB, GB, instead of
             # their size in bytes (octets).
    ls -lha  # Adding the "-a" option additionally displays hidden files and
             # directories. These are files/directories whose name starts with
             # a dot ".".
             # Hidden files are often used to store program configurations.
    ```

5. List the content of the directory in chronological and reverse chronological
   order.

    ```sh
    ls -lht    # The "-t" option sorts by time, newest file first.
    ls -lhtr   # The "-r" option reverses the order of sorting.
    ```

    Some other useful `ls` options and shortcuts:

    ```sh
    ls -a/--all  # Also show hidden files.
    ls -R        # --recursive, list subdirectories recursively.
    
    cd .         # Does nothing, we stay in the same directory.
    cd ..        # Go to parent directory.
    cd /         # Go to root directory.
    cd ~         # Go to user's home directory, on Linux: /home/<user name>.
    cd -         # Go back to the previous directory.
    cd           # With no argument, cd brings you back to your home directory.
    ```

</p>
</details>
<br>

### Additional Tasks 1

6. **Try the `cd ~` and `cd -` shortcuts**. What do they do?

7. **Create an alias named `ll`** that runs the following command:
   `ls -lh --group-directories-first --color=auto`.

   :sparkles:
   *Notes:*
   * On some Linux system, an `ll` alias may already exist.
   * To list your currently defined aliases, you can type `alias` to list them
     all, or `alias <name of alias>` to list a specific one (e.g. `alias ll`).
   * Aliases are only valid within your current shell session. To make aliases
     permanent, they must be defined inside a configuration file, such as
     `~/.bashrc`, so that they get loaded each time a new shell is spawned.
   * To remove an alias we use `unalias <alias name>`, or we remove it from
     the config file where it is defined.

8. **Compute the size of a directory**. To display the size of a directory,
   the command **`du -sh <directory>`** can be used. Try in on the directories
   found in `exercise_1`.

9. Let's look at a detail of how the bash shell displays file sizes.

   Go into the directory `a_directory` and list its content using the
   following commands - look at how file size is indicated:
   * `ls -l`: lists the file size in bytes/octets.
   * `ls -lh` (you can also use your new `ll` alias!): lists the file size in
              a more readable format, using the `k`, `M`, `G`, ...
              unit abbreviations for `kB` (kilobyte), `MB` (megabyte), `GB`,
              (gigabyte) etc.

   :sparkles:
   *Note:* in everyday language, the term **kilobyte** (abbreviated `kB`) is
   used for talking interchangeably about either 1000 bytes or 1024 bytes,
   because they represent almost the same quantity of bytes.
   If we really wanted to be precise, the proper name for a unit of 1024 bytes
   is a *kibibyte* `KiB`, while a *kilobyte* designates 1000 bytes. Similarly,
   a *megabyte* is 1'000'0000 bytes, and a *mebibyte* is 1024^2 bytes (same
   with *gigabyte* vs. *gibibytes*, *terabyte* vs.*tebibyte*, etc.).

<br>
<details><summary><b>Additional tasks solution</b></summary>
<p>

6. `cd ~` and `cd -` shortcuts:
   * **`~`** is a shortcut for the "home directory", and therefore `cd ~` is a
     shortcut to change directory to your home directory.
   * **`-`** is a shortcut to change to the previous working directory. It is
     handy if you want to return to a directory you were in just previously.

7. Create an `ll` alias:

    ```sh
    # Create a new "ll" alias:
    alias ll='ls -lh --group-directories-first --color=auto'
    ```

   Here are some some more useful commands for aliases:

    ```sh
    alias       # Lists the currently defined aliases.
    unalias ll  # Removes the alias from the current shell session.
    type ll     # The "type" command tells if a command is an alias, or shows
                # the path to the binary file.
                # -> ll is aliased to `ls -lh --group-directories-first --color=auto'
    type bash   # -> bash is /usr/bin/bash
    ```

8. Show the size of the directories:

     ```sh
     du -sh a_directory  # 20 K (20 kilobytes)
     du -sh b_directory  # 4K   (directory is empty, 4K is the size of an empty dir)
    
     # Using the ? wildcard character, we can also compute the size of both
     # directories in a single command.
     du -sh ?_directory
     ```

9. Nothing to correct.

</p>
</details>

<br>
<br>
<br>

## Exercise 2 - File globbing with wildcard characters [20 min]

**Objective:** learn to use **wildcard characters** to match existing file
names.

:sparkles:
**Notes:**

* The technical term for the expansion of wildcards characters by the shell is
  **[filename expansion](https://www.gnu.org/software/bash/manual/bash.html#Filename-Expansion)**,
  but it is also very often referred to as **globbing**.
* Globbing only matches **existing file/directory names**: expansion will not
  happen is there is no matching file/directory. This is why it's official
  name is *filename expansion*!
* If you don't want a specific wildcard character to expand, you can
  **escape it** by prefixing it with `\`. E.g. `ls test_\*.md` will try to
  list a file named exactly `test_*.md`.

To start this exercise, enter the directory `exercise_2/RedList_mammals` and
list its content with the command **`ls`**.
You will see that it contains a large number of files, whose names are those
of the critically endangered mammal species as listed in the
[International Union for Conservation of Nature (IUCN) Red List](https://www.iucnredlist.org).

The species names are given in
[binomial nomenclature (i.e. latin names)](https://en.wikipedia.org/wiki/Binomial_nomenclature),
and each file has the structure `Genus_species`. E.g. if there a was file for
humans, it would be named `Homo_sapiens`.

**Using `ls` and wildcard characters, perform the following tasks:**

1. List all files starting with the letter `i` (upper or lower case).  
   :dart:
   **Hint:** you should have 1 match.

2. List the files of [Rhinoceros species](https://en.wikipedia.org/wiki/Rhinoceros#Species)
   (genus *Rhinoceros*, *Dicerorhinus*, and *Diceros*).  
   :dart:
   **Hint:** you should have 3 matches.

3. List the files of Gibbon species from the genus
   *[Nomascus](https://en.wikipedia.org/wiki/Nomascus)* whose species
   name ends with either `r` or `i`.  
   :dart:
   **Hint:** you should have 2 matches.

4. List the files of species that meet *both* following conditions:
   * The genus name contains the pattern "`l` + a single letter + a letter
     between `a` and `h`", e.g. `lia` or `lug`.
   * The species name starts with a `g`.

   For instance, *Eubalaena glacialis*, the
   [North Atlantic right whale](https://en.wikipedia.org/wiki/North_Atlantic_right_whale),
   would be a match, because its genus name *Eubalaena* contains the pattern
   `lae` and its species name *glacialis* starts with a `g`.  
   :dart:
   **Hint:** you should have 3 matches.

<br>

<details><summary><b>Exercise solution</b></summary>
<p>

1. There is only one file that starts with the letter `i`:

    ```sh
    cd exercise_2/RedList_mammals/
    ls -l I*        # Returns a single match: Indri_indri (a lemur species)
    ```

    :sparkles:
    Since all file names start with a capital letter, `ls -l I*` is sufficient
    to list all files starting with the letter `i`. If there were also files
    starting with lower case letters, we would use `ls -l [iI]*`

    :warning:
    Please note that `ls -l [iI]*` and `ls -l i* I*` are not completely
    equivalent expressions: `ls -l i* I*` will return an error unless there are
    both files starting with `i` and `I` (you can test it in your terminal).

2. The critically endangered Rhino species are:

    ```sh
    ls -l Rhinoceros_* Dicerorhinus_* Diceros_*
    ls -l Rhinoceros* Dicero*                     # Gives the same result.

    # Dicerorhinus_sumatrensis  (Sumatran Rhinoceros)
    # Diceros_bicornis          (Black Rhino)
    # Rhinoceros_sondaicus      (Javan Rhinoceros)
    ```

   :sparkles:
   Since both the genus `Dicerorhinus` and `Diceros` start with `Dicero`,
   we can match the pattern `Dicero*` to get both genuses at the same time.

   :rhinoceros:
   There exists 2 other Rhino species:
   * The White Rhino (*Ceratotherium simum*) is
     [listed as "Near Threatened" by the IUCN](https://www.iucnredlist.org/species/4185/45813880).
     This species has two subspecies: the Northern and Southern White Rhino.
     The Northern White Rhino subspecies is critically endangered with only 2
     female individuals remaining worldwide (living in semi-captivity in Kenya).
   * The Greater One-Horned Rhino (a.k.a. Indian Rhino), *Rhinoceros unicornis*
      is [listed as "Vulnerable" by the IUCN](https://www.iucnredlist.org/species/19496/18494149).

3. [Gibbon Nomascus species](https://en.wikipedia.org/wiki/Nomascus) whose
   species name ends in `r` or `i`:

    ```sh
    ls -l Nomascus_*[ri]

    # Nomascus_concolor  (Black crested gibbon).
    # Nomascus_siki      (Southern white-cheeked gibbon).
    ```

4. Species matching both conditions:

    ```sh
    ls -l *l?[a-h]*_g*

    # Eubalaena_glacialis    (North Atlantic right whale).
    # Gorilla_gorilla        (Western gorilla).
    # Plecturocebus_grovesi  (Alta Floresta titi monkey - a new world monkey)
    ```

</p>
</details>

<br>

### Additional Tasks 2

5. List the files of species who satisfy both of the following conditions:
   * The genus name contains the pattern "`a` or `o`, followed by exactly 2
     letters, followed by the letter `x`" (e.g. `abix` or `onyx`)
   * The species name ends either with an `i` or with the pattern `ra`.

   For instance, *Pteralopex pulchra*, the
   [Montane monkey-faced bat](https://en.wikipedia.org/wiki/Montane_monkey-faced_bat),
   would be a match, because its genus name *Pteralopex* contains the pattern
   `opex` and its species name *pulchra* ends with the pattern `ra`.

   :dart:
   **Hint:** this cannot be matched in a single expression only with regular
   file globbing (i.e. filename expansion). You will need to either i) use
   2 expressions with regular globbing, ii) use
   [brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion),
   or iii) use
   [pattern matching](https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching).

   :dart:
   **Hint:** you should have 4 matches.

6. Try to add quotes (single or double) around a globbing pattern with
   wildcards, e.g. `ls -l "I*"`:
   * What difference does it make (if any)?
   * Can you think of a use case for using quotes around a pattern with
     wildcards?

<br>

<details><summary><b>Additional tasks solution</b></summary>
<p>

5. File names matching the requested criteria:

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
    To avoid duplicating the `*[ao]??x_*` part, we can use either
    **pattern matching** or **brace expansion**.

    * **[Pattern matching](https://www.gnu.org/software/bash/manual/bash.html#Pattern-Matching)**:
      here `@(ra|i)` matches either the pattern `ra` or `i`.
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

      Before the actual globbing is performed.

6. Adding single or double quotes around the search pattern prevents the
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

</p>
</details>

<br>
<br>
<br>

## Exercise 3 - Creating and moving directories and files [20 min]

**Objective:** learn to use the **`mkdir`**, **`cp`** and **`mv`** commands.

Enter the directory `exercise_3/` and perform the following tasks:

1. **Create directories** with the **`mkdir`** command:
   * In the directory `exercise_3/`, create 2 new sub-directories:
     `species_by_genus` and `species_by_common_name`.
   * In `species_by_genus/`, create 2 new sub-directories:
     `Dendrolagus` ([tree-kangaroos](https://en.wikipedia.org/wiki/Tree-kangaroo))
     and
     `Crocidura` ([a genus of shrews](https://en.wikipedia.org/wiki/Crocidura)).
   * In `species_by_common_name/`, create 2 new sub-directories
     named `B`, and `R`.

2. **Copy files** using the **`cp`** command:
   * From the directory `exercise_2/RedList_mammals`, make a copy of all files
     of the genuses `Dendrolagus` and `Crocidura` into their respective
     sub-directories in `species_by_genus`.
   * From the directory `exercise_2/RedList_mammals`, copy the file for the
     [Red Wolf](https://en.wikipedia.org/wiki/Red_wolf) (*Canis rufus*) to the
     directory `species_by_common_name`.

3. **Move and rename files** with the **`mv`** command:
   * Enter the `species_by_common_name` directory.
   * In the directory, move the file `Canis_rufus` into subdirectory `R`.
   * Rename the `Canis_rufus` file you just moved into the subdirectory `R` to
     the common name of the species: `Canis_rufus` -> `Red_wolf`.

4. **Copy and rename files** with the **`cp`** command:
   * Similarly to what we did for the Red Wolf file, we will now copy and
     rename the file for the
     [Black Rhinoceros](https://en.wikipedia.org/wiki/Black_rhinoceros)
     *Diceros bicornis*, but this time we will copy and rename the file
     *in a single step* using the `cp` command.
   * Copy the file `Diceros_bicornis` from its original location (in
     `exercise_2/RedList_mammals`) into `species_by_common_name/B`, while
     directly renaming it to the common name of the species: `Black_rhino`.

5. **Copy, rename and delete directories**:
   * Change directory to the root of the `exercise_3/` directory.
   * Copy the entire directory `species_by_genus/Dendrolagus/` with all its
     content to the root of `exercise_3`.
   * Rename the directory to `Tree-kangaroos`.
   * Delete the directory `Tree-kangaroos` and its content **in a safe way**.

<br>

<details><summary><b>Exercise solution</b></summary>
<p>

1. Create the `species_by_genus` and `species_by_common_name`
   directories.

     ```sh
     cd exercise_3

     # Option 1: create one directory after the other.
     mkdir species_by_genus
     mkdir species_by_common_name

     # Option 2: create both directories with a single command.
     mkdir species_by_genus species_by_common_name

     # Option 3: use brace expansion to avoid repeating the common part
     #           of the directory names.
     mkdir species_by_{genus,common_name}
     ```

   Create sub-directories `Dendrolagus` and `Crocidura`:

     ```sh
     # Option 1: create sub-directories while in the exercise_3 directory.
     mkdir species_by_genus/Dendrolagus species_by_genus/Crocidura

     # Option 2: enter the species_by_genus directory, then create the
     #           sub-directories "Dendrolagus" and "Crocidura".
     cd species_by_genus/
     mkdir Dendrolagus Crocidura
     cd ..

     # Option 3: same as option 1, but using brace expansion to avoid repetition.
     mkdir species_by_genus/{Dendrolagus,Crocidura}
     ```

   Create sub-directories `R` and `B`:

    ```sh
    mkdir species_by_common_name/{R,B}
    ```

   :sparkles:
   *Note:* using the `-p` option of `mkdir`, it is possible to create
   multiple levels of directories in a single command. For example, we could
   create all the directories for this exercise in a single command:

    ```sh
    mkdir -p species_by_{genus/{Dendrolagus,Crocidura},common_name/{R,B}}
    ```

    :fire:
    *Tip:* if you want to preview the output of a brace expansion by
    the shell, you can run the command prefixed with `echo`: it will print
    the command that would be executed to the terminal without running the
    command.

    ```sh
    echo mkdir -p species_by_{genus/{Dendrolagus,Crocidura},common_name/{R,B}}
    ```

2. Copy files for `Dendrolagus` and `Crocidura`:

    ```sh
    cp ../exercise_2/RedList_mammals/Dendrolagus_* species_by_genus/Dendrolagus/
    cp ../exercise_2/RedList_mammals/Crocidura_* species_by_genus/Crocidura/
    ```

   Copy the file for the Red Wolf:

    ```sh
    cp ../exercise_2/RedList_mammals/Canis_rufus species_by_common_name/
    ```

3. Move and rename the Red Wolf file:

    ```sh
    cd species_by_common_name/
    mv Canis_rufus R/            # Move the file into its subdirectory.
    mv R/Canis_rufus R/Red_wolf  # Rename the files to the common name of the species.
    ```

4. Copy and rename the file for the Black Rhino in a single `cp` command:

     ```sh
     # Note: this assumes you are currently in directory "species_by_common_name".
     cp ../../exercise_2/RedList_mammals/Diceros_bicornis B/Black_rhino
     ```

5. Copy, rename and delete a directory:

    ```sh
    cd ..                                  # Change directory to `exercise_3`.
    cp -r species_by_genus/Dendrolagus/ .  # Copy the directory and its content.
    mv Dendrolagus/ Tree-kangaroos         # Rename the directory.
    ```

    To delete the directory in a safe way, we first delete all the files
    inside it, and then delete the empty directory with `rmdir`.
    Note that `rmdir` will not delete a directory if it's not empty - this
    is a safety behavior to avoid deleting large number of files by mistake.

    ```sh
    rm Tree-kangaroos/*
    rmdir Tree-kangaroos
    ```

    :kangaroo:
    *Note:* the faster way to delete the directory and all of its content is
    to use the command: `rm -rf Tree-kangaroos`.
    * :warning:
      This recursively delete the directory, and therefore one has to be
      careful to delete the correct directory, as you can otherwise very
      quickly delete large amounts of data by mistake, which can be problematic
      as **there is no command to undo file deletion**.

</p>
</details>

<br>

### Additional Tasks 3

* At the root of `exercise_3/`, create a new directory named
  `species_by_binomial_name` and enter it.

* Inside this directory, create sub-directories named `A`, `B`, `C`, ... `Z`
  (i.e. one directory for each letter of the alphabet).

  To avoid doing this tedious work manually, you can use a **for loop** very
  similar to this example:

    ```sh
    for x in {A..Z}; do echo ${x}; done
    ```

  Try to run the above code in your shell (it will only print things to the
  screen without creating anything on disk). Then adapt the `for` loop so
  that it creates the directories for `A` to `Z`.

* Using a similar `for` loop again, copy all files from
  `exercise_2/RedList_mammals` into their correct subdirectory, i.e. the
  subdirectory that corresponds to the first letter of the Genus name.
  For example: `Marmota_vancouverensis` should go into sub-directory `M`
  because the first letter of the genus name is `M`.

  Note that when running the for loop, you will get some **warning messages**,
  because the genuses present in `RedList_mammals` do not cover all letters
  of the alphabet. However, this is not a problem here because it does not
  prevent the `for` loop from running to the end.

<br>

<details><summary><b>Additional tasks solution</b></summary>
<p>

```sh
# Create and enter the new directory.
mkdir species_by_binomial_name
cd species_by_binomial_name/

# Create directories "A" to "Z" with a for loop.
for x in {A..Z}; do mkdir ${x}; done

# Copy species file names into the correct directory.
# Note that letters that do not have any matching genus will print a warning
# to the terminal, but this does not prevent the loop from completing.
for x in {A..Z}; do cp ../../exercise_2/RedList_mammals/${x}* ${x}/; done
ls -l ./*
```

:sparkles:
The task of creating all the directories could also be done using
[brace expansion](https://www.gnu.org/software/bash/manual/bash.html#Brace-Expansion),
like so:

```sh
mkdir {A..Z}
```

</p>
</details>

<br>
<br>
<br>

## Exercise 4 - Finding files [15 min]

**Objective:** learn to use the **`find`** command.

Go to the root of the directory `exercises/` and perform the following
tasks using the `find` command:

1. **Find all files with a `.png` extension** located anywhere in `exercises/`.
   Make sure to list *only* files, and not directories.  
   :dart:
   **Hint:** you should find a total of 6 files.

2. **Find files with either a `.jpeg` or `.png` extension**. As before,
   directories should be excluded from the search results.  
   :dart:
   **Hint:** you should find a total of 15 files.

3. Find all `.jpeg` files **larger than `15 kB`**.

<br>

<details><summary><b>Exercise solution</b></summary>
<p>

1. Find all `.png` files. We use **`-type f`** to restrict the search to
   files (and exclude directories).

     ```sh
     cd /path/to/directory/exercises  # Make sure to be in the correct directory.
     find . -type f -name *.png
     # -> There are 6 ".png" files, located in ./images/img.png/
     ```

2. Find all `.jpeg` or `.png` files. We use the `-or` operator to combine both
   conditions. Note that the `-type f` must be repeated for each condition.

     ```sh
     find . -type f -name *.png -or -type f -name *.jpeg
     # -> There are 9 ".jpeg" files, located in ./images/img.jpeg/
     # -> There are 6 ".png" files, located in ./images/img.png/
     ```

3. Find all `.jpeg` files larger than `15 kB`.

    ```sh
    find . -type f -name *.jpeg -size +15k
    ```

</p>
</details>

<br>

### Additional Tasks 4

Try to use the **`-exec` option** of `find` to display full details of the
files that are found in the point 3 of the main exercise above.

One possible way to use the `-exec` options is as follows:

* **`-exec <command> "{}" +`**, where `<command>` is the custom command to
  execute and `"{}"` is expanded to the files found by `find`.

The expected output for all `.jpeg` files larger than `15 kB` looks like this:

```sh
-rw-rw-r-- 1 bob bob 25K Jan  8 11:16 ./images/img.jpeg/linux_logo.jpeg
-rw-rw-r-- 1 bob bob 26K Jan  8 11:40 ./images/img.jpeg/linux_gentoo_logo.jpeg
-rw-rw-r-- 1 bob bob 16K Jan  8 11:36 ./images/img.jpeg/linux_suse_logo.jpeg
```

<br>

<details><summary><b>Additional tasks solution</b></summary>
<p>

```sh
find . -type f -name *.jpeg -size +15k -exec ls -lh "{}" +
```

:sparkles:
The following syntax is also possible:

```sh
find . -type f -name *.jpeg -size +15k -exec ls -lh "{}" \;
```

In this case, the shell will execute an individual `ls -l` command for each
file that was found, rather than passing all files to `ls -l`. In the case of
the `ls` command, this does not change anything, but there are commands that
accept only a single file as argument, in which case the solution with
`"{}" +` would not work because all files are passed to the command in a
single call.

</p>
</details>

<br>
<br>
<br>

## Exercise 5 - Display file content [10 min]

**Objective:** get familiar with shell commands that display text file content:
**`head`**, **`tail`**, **`cat`** and **`less`**.

From the root of the `exercises/` directory, locate the file
`protein_sequences.fasta` using the **`find`** command and navigate to it.  
Then perform the following tasks:

1. **Display the start/end of the file** using the **`head`** and **`tail`**
   commands:
   * Display the first 10 lines of the file.
   * Display the last 5 lines of the file.

2. **Count the number of lines** in the file using the **`wc`** command:
   * Count only the number of lines in the file.
   * Count only the number of words in the file.

3. **Display the content** of the file using the **`cat`** command:
   * Why is this not the most adapted program here?
   * Indicate another usage of cat?

4. **Display, navigate and search** the file with **`less`**:
   * Open the file using `less`.
   * Add lines numbers to the display using the `-N` option.
   * Navigate the file using the space bar and arrows.
   * Search for the pattern `isoform` using the command `/<search term>`, then
     navigate through the matches with the keys `n` and `N`.
   * Close the file with `q`.

<br>

<details><summary><b>Exercise solution</b></summary>
<p>

0. Locate the file `protein_sequences.fasta` and navigate to it.

    ```sh
    find . -name "protein_sequences.fasta"
    cd ./exercise_5/fasta_files/
    ```

1. Display the first 10 and last 5 lines.

    ```sh
    head protein_sequences.fasta      # No need to specify -n 10 in this case
                                      # because 10 is the default value.
    tail -5 protein_sequences.fasta
    ```

   :fire:
   **Tips:**
   * If you want to display the entire file except for the last `X` lines you
     can use `head -n-X` (replace `X` by the number of lines you want to skip
     at the end of the file).
   * Conversely, `tail -n+X` will skip the first `X` lines, and then print all
     the remaining lines till the end of the file.

2. Count the number of lines and words in the file.

    ```sh
    wc -l protein_sequences.fasta   # 19222 lines.
    wc -w protein_sequences.fasta   # 51914 words.
    ```

3. Display the content of the file with `cat`. As you can see, this is not
   an ideal solution for this file because it is large.

    ```sh
    cat protein_sequences.fasta
    ```

   One usage of **`cat`** is con**cat**enate 2 or more files together (this is
   where the command got its name from). `cat` concatenates files by pasting
   their content one after another.  
   Here is an example:

   ```sh
   # Create 2 files to concatenate:
   head -n5 protein_sequences.fasta > file_1
   tail -n5 protein_sequences.fasta > file_2

   # Concatenate our 2 files into a file named "file_3".
   cat file_1 file_2 > file_3
   cat file_? > file_3         # Same as above, but using filename globbing.
   ```

   :sparkles:
   Bonus: we could also create `file_3` without using any intermediate file.
   The `<(  )` syntax is called
   **[process substitution](https://www.gnu.org/software/bash/manual/bash.html#Process-Substitution)**
   and allows to treat the output of a command as an input file.

   ```sh
   cat <( head -n5 protein_sequences.fasta ) <( tail -n5 protein_sequences.fasta )
   ```

   :sparkles:
   To concatenate multiple files by columns, use the **`paste`** command.

4. Display the content of the file with `less`. Remember that to exit `less`,
   you must press the `q` key on your keyboard.

    ```sh
    less protein_sequences.fasta
    less -N protein_sequences.fasta   # Line numbers can also be added/removed
                                      # after a file was opened with "-N" + "enter".
    ```

</p>
</details>

<br>

### Additional Tasks 5

Display *only* the line 100 of the file `protein_sequences.fasta` by using a
combination of `head` and `tail`.
For this you will need to use the the `|` (pipe) operator, that allows to
redirect the output of one command into another command.

<br>

<details><summary><b>Additional tasks solution</b></summary>
<p>

`head` and `tail` can be combined to display any section of a file. Here
we print the line 100 of the file:

```sh
head -n100 protein_sequences.fasta | tail -n1  # Print the 100th line.
```

</p>
</details>

<br>
<br>
<br>

## Exercise 6 - Merge data in columns [30 min]

**Context:** in this exercise, we will be working with 3 files containing
replicates from a
[micro-array experiment](https://en.wikipedia.org/wiki/DNA_microarray). They
are located in `exercise_6`:

* `micro-array/data/array_data-1.csv`
* `micro-array/data/array_data-2.csv`
* `micro-array/data/array_data-3.csv`

To get an overview of the structure of these files, you can have a look at
the start of each file with `head array_data-*` (you need to be in the
directory `exercise_6/micro-array/data/` to run this command).

Each file contains 2 columns, separated by `;` characters:

* **Column 1:** gene name (`ProbeID`).
* **Column 2:** level of gene expression in each replicate
  (`Sample1`, `Sample2`, `Sample3`).

```sh
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

**Our objective** is to merge these three files into a single tab-delimited
file with 4 columns: `ProbeID` (gene name), `Sample1`, `Sample2` and `Sample3`
(the gene expression levels recorded in each replicate of the experiment).

Additionally, the output file should contain tab-delimited values rather than
semi-column separated values as is the case in the input files.

Our final output should thus look something like this:

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
values from the input files will have to be sorted before the columns can be
merged.

As this exercise is a bit more complicated, we will decompose it into several
steps.

<br>

### Step 1: data exploration

Enter the directory `exercise_6/micro-array/data` and have a look at the
3 input files using `less` or `head`, to get familiar with their structure
and content.

<br>

### Step 2: conversion to tab-delimited values

The original files contain tabulated data separated by a `;` (semi-column)
character.

* Convert the delimiters from `;` to `\t` (tab).
* Save the converted content into a new file with a `.tsv` extension. E.g. the
  converted version of `array_data-1.csv` should be named `array_data-1.tsv`.

<details><summary><b>Step 2 solution</b></summary>
<p>

```sh
tr ";" "\t" < array_data-1.csv > array_data-1.tsv
tr ";" "\t" < array_data-2.csv > array_data-2.tsv
tr ";" "\t" < array_data-3.csv > array_data-3.tsv
head *.tsv

# Loop shortcut:
for i in $(seq 1 3); do tr ';' '\t' < array_data-${i}.csv > array_data-${i}.tsv; done
```

:penguin:
*fun fact:* `tr` is one of the (few) commands that does not accept a file as
input, it only accepts input from *stdin*. This is why we must use `tr < file`
or `cat file | tr` to pass input to `tr`.

</p>
</details>

<br>

### Step 3: sort the files

Before we can merge the content of the 3 `array_data-*.tsv` files, we have to
make sure that the order of rows in each file (i.e. the order of genes) are the
same.

If you look at the files, you will see that this is not the case. Therefore the
files need to be sorted by their 1st column (`ProbeID`).

* Sort each `array_data-*.tsv` file by its `ProbeID` column using the
  **`sort`** command.
* Make sure that the **header line** of the file remain at the top after the
  sorting operation.  
  :dart:
  **Hint:** the header line is the only one that starts with a letter, so we
  can take advantage of *numerical sorting* that sorts letters before numbers.
  You can have a look at `man sort` (the help for the `sort` command) to find
  the right option.
* Save the sorted output to files named `array_data-sorted-*.tsv`.

<details><summary><b>Step 3 solution</b></summary>
<p>

```sh
sort -n array_data-1.tsv > array_data-sorted-1.tsv
sort -n array_data-2.tsv > array_data-sorted-2.tsv
sort -n array_data-3.tsv > array_data-sorted-3.tsv
head *sorted-?.tsv

# Loop shortcut:
for i in $(seq 1 3); do sort -n array_data-${i}.tsv > array_data-sorted-${i}.tsv; done
```

</p>
</details>

<br>

### Step 4: verify the file sorting

In this step, we will simply double-check that the sorted files we created
at the previous step (`array_data-sorted-*.tsv`) have the same number of lines
and that the genes on those lines are in the same order.

To verify this, the idea is to extract the first column (the gene names) from
the sorted files, and compare it across the 3 sorted files.

Proceed as follows:

* Use the **`cut`** command to extract the first column (`ProbeID`) of each
  `array_data-sorted-*.tsv` file. Save the output to temporary files named
  `tmp-1.tsv`, `tmp-2.tsv`, and `tmp-3.tsv` (these files should contain a
  single column).
* Compare the content of the 3 `tmp-*.tsv` files using the commands
  `diff -s tmp-1.tsv tmp-2.tsv` and `diff -s tmp-1.tsv tmp-3.tsv`.
* If all `tmp-*.tsv` files are the same (and they should), you can now delete
  these files. Their only purpose was to allow us to check that all files
  have their lines sorted in the same order.

<details><summary><b>Step 4 solution</b></summary>
<p>

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
where the output of a command is treated as a sort of *virtual file*.

```sh
diff -s <(cut -f1 array_data-sorted-1.tsv) <(cut -f1 array_data-sorted-2.tsv)
diff -s <(cut -f1 array_data-sorted-1.tsv) <(cut -f1 array_data-sorted-3.tsv)
```

</p>
</details>

<br>

### Step 5: Merge the sorted files

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

<details><summary><b>Step 5 solution</b></summary>
<p>

```sh
paste array_data-sorted-*.tsv | cut -f 1,2,4,6 > final.tsv
head final.tsv
```

:sparkles:
*Note:* to learn how to do the entire processing we did in this exercise
**in a single command**, look at the Additional Tasks 6 section below. It
also shows how the processing can be done using the `join` command, but it's
actually more complicated in this case.

</p>
</details>

<br>

### Additional Tasks 6

Try to re-write the entire process as a single command. For this you will
need to use the following shell functionalities:

* The **Pipe operator `|`**, to redirect the input of one command into the
  next.
* The **[process substitution](https://www.gnu.org/software/bash/manual/bash.html#Process-Substitution)**
  syntax `<( command )`, to treat the output of a command (or of a series of
  commands) as a virtual file from which data is read.

This task is a bit more complicated, so to get you started, here is an example
to give you some inspiration. You can run the command bellow in your shell:

```sh
paste <(sort -n array_data-1.csv | cut -f2 --delim=";") <(sort -n array_data-2.csv | cut -f2 --delim=";") | head
```

<br>

<details><summary><b>Additional tasks solution</b></summary>
<p>

Here is how we could do the whole processing of this exercise in a single
command without creating any intermediate files.

```sh
paste <(sort -n array_data-1.csv | tr ";" "\t") \
      <(sort -n array_data-2.csv | cut -f2 --delim=";") \
      <(sort -n array_data-3.csv | cut -f2 --delim=";") > final_2.tsv

# Compare the new output file with the one we produced earlier:
diff -s final*.tsv
diff -s final{,_2}.tsv
```

Another alternative is to use the **`join`** command. Unfortunately, the `join`
command only allows to join 2 files at a time, so in this case the solution
ends-up being more complicated (`join` would however be much better in cases
where we want to join files that have missing rows - i.e. not all files have
all the raws):

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

</p>
</details>

<br>
<br>
<br>

## Exercise 7 - using `grep` to retrieve information from files [30 min]

In this exercise, we will work with a copy of the file
`exercise_5/fasta_files/protein_sequences.fasta`. This file is a so-called
[FASTA file](https://en.wikipedia.org/wiki/FASTA_format). FASTA is a
text-based format to represent nucleotide or protein sequences.

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

Enter the directory `exercise_7` and start by making a copy of the file
`exercise_5/fasta_files/protein_sequences.fasta` in that directory. Name
the copy of the file `sequences.fasta`.

:sparkles:
If you are on a Linux/Mac, you may also create a **symlink** instead of
copying the file:
`ln -s ../exercise_5/fasta_files/protein_sequences.fasta sequences.fasta`
A symlink creates a pointer to a file, without making an actual copy of it.
Symlinks are not supported on Windows (except if using WSL an working on a
non-windows partition).

Have a look at the `sequences.fasta` file (e.g. using the `less` command).
Then answer the following questions using the `grep` command:

* How many sequences are there in the file? :dart: **Hint:** count the number
  of header lines in the file.
* How many entries are from `Staphylococcus`?
* Display header lines that are *not* from `Staphylococcus`?

Here is a reminder of some of the `grep` options:

* `-i`: case insensitive search.
* `-c`: suppress normal output; instead print the count of matching lines.
* `-o`: print only matching content, not the entire line.
* `-n`: add the line number in front of printed output.
* `-v`: inverted search - print lines that do *not* match the pattern.

<br>

<details><summary><b>Part A solution</b></summary>
<p>

```sh
cd exercise_7/
cp ../exercise_5/fasta_files/protein_sequences.fasta sequences.fasta


# Count the number of sequences in the file:
grep -c "^>" sequences.fasta   # -> 3325 sequences.

# Count the number of sequences from Staphylococcus
# Note the use of the `-i` option of `grep` ("case insensitive search").
grep -ci "os=staphylococcus " sequences.fasta   # 141 sequences.

# Display the header lines of sequences that are not from Staphylococcus.
grep "^>" sequences.fasta | grep -vi "os=staphylococcus "
grep "^>" sequences.fasta | grep -vi "os=staphylococcus " | wc -l   # The sequence count is 3184.
```

</p>
</details>

<br>

### Part B - extract the top 10 most-frequent genus

In the second part of this exercise, your task is to display the 10 most
frequent genuses in the sequences of the `sequences.fasta` file, along with
their frequency (i.e. the number of sequences for each of the 10 most-frequent
genus in the file).

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

* The steps above are best done as part of a pipeline: use the `|` (pipe)
  operator to pipe the output of one command into the next.
* When building the pipeline and doing tests, you can end your pipeline with
  `| head` so that you avoid printing the whole file each time.

:dart:
**Additional hints:**
<details><summary><b>click to show more hints, if needed</b></summary>
<p>

Here are some commands and their options that are useful for this exercise:

* `uniq -c`: the `-c/--count` option prefixes each line with the number of
             occurrences.
* `sort -nr`: `-n/--numeric-sort` sorts numerically instead of alphabetically.
              `-r/--reverse` sorts in decreasing order.
* `grep -o`: the `-o/--only-matching` option returns only the matching part of
  a line instead of the entire line (the default grep behavior).

</p>
</details>

<br>

<details><summary><b>Part B solution</b></summary>
<p>

There are multiple ways to perform this task, here are a few possibilities.

Here are 3 different variants using a pipeline built around `grep` and `cut`.

* :sparkles:
  *Note:* some pipelines make use of the `grep` option **`-o`**, which
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

* Using `grep` with "Perl"-style regular expressions by adding the `-P` option.
* Use a **lookbehind match**: `(?<=OS=)` matches something located behind the
  pattern `OS=`.

```sh
grep -oP "(?<=OS=)[a-zA-Z]+ " sequences.fasta | sort | uniq -c | sort -nr | head
```

:see_no_evil:
**[Regular expressions](https://en.wikipedia.org/wiki/Regular_expression)** are
a powerful tool to do sophisticated pattern matching. However they are beyond
the scope of this course.

</p>
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
  iterating over a range of values.
  In our case, we want to iterate over the list of genuses.
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

<details><summary><b>Additional tasks solution</b></summary>
<p>

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

</p>
</details>

<br>
